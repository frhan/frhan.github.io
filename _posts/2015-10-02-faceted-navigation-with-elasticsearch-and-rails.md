---
layout: post
title: Faceted navigation with Elasticsearch and Rails
categories: [rails,elasticsearch]
description: create sample project which will search post and facet location and categories
keywords: rails,elasticsearch
---

### In this article I am going to create sample project which will search post and facet location and categories.

Searching and faceting are very common in ecommerce and job sites.Here I use Elasticsearch and Rails 4. Finally the result will be like this ..

![alt text](https://raw.githubusercontent.com/frhan/frhan.github.io/master/public/images/image_1.png)

First create a **new** project

```ruby
 rails new RailsPostSearch
```

The main model of this project is **Post**. So create the model first. Run the command.

```ruby
 rails g model Post title:string desc:text price:decimal image:string 
```

run the migration ..

```ruby
 rake db:migrate 
```

Create the location model.

```ruby
 rails g model Location name:string desc:text
```
 
Create the category model.
 
```ruby
 rails g model Category name:string desc:text
```
 
run the migration ..

```ruby
 rake db:migrate 
```

Any post should have a location and belongs to multiple categories.So update the **post** model ```/app/models/post.rb```

```ruby
 class Post < ActiveRecord::Base
  belongs_to :location
  has_and_belongs_to_many :categories
  
  validates_presence_of :title
  validates_presence_of :location
 end
```

update **Location** model ```/app/models/location.rb```.

```ruby
 class Location < ActiveRecord::Base
   has_many :posts
 end
```

update **Category** model ```/app/models/category.rb```.

```ruby
 class Category < ActiveRecord::Base
  has_and_belongs_to_many :posts
 end
```

Now we need add some gems. update ``` Gemfile ```. Add the following gems.

```ruby
 gem 'bootstrap-sass'
 gem "kaminari"
 gem 'elasticsearch-model'
 gem 'elasticsearch-rails'
```
now run 

```ruby
 bundle install
```

we added bootstrap as css framework.so we need to update the javascript and css file.
update ```app/assets/javascript/application.js``` file

```javascript
 //= require jquery
 //= require bootstrap-sprockets
 //= require jquery_ujs
 //= require turbolinks
 //= require_tree .
```

update ```app/assets/stylesheets/application.scss``` file. Add following lines

```css
 @import "bootstrap-sprockets";
 @import "bootstrap";
```

run following command for integrating **bootstrap3** with **kaminari**.

```ruby
 rails g kaminari:views bootstrap3
```

create controller for **Post**. 

```
rails g controller Post index 
```
create partial view file of **Post**. ```app/views/posts/_post.html.erb``` 

```html
<div class="col-sm-12 col-md-12 thumbnail">
  <div class="thumbnail">
    <%= image_tag post.image %>
  </div>
  <div class="caption">
    <h3><%= link_to post.title, post_path(post.id) %></h3>

    <p><%= post.desc %>></p>

    <p>
      <label><%= post.location.name %></label>
      <label> Category: </label>
      <% post.categories.each do |category| %>
          <label><%= category.name %></label>
      <% end %>
    </p>
  </div>
</div>
```

Now I am going to implement the **elasticsearch** on this project.Include the elasticsearch implementation as concern.
I made Location and categories as Facet. add the code ```app/models/concern/searchable.rb````

```ruby
module Searchable
  extend ActiveSupport::Concern

  included do
    include Elasticsearch::Model

    # Customize the index name
    #
    index_name Rails.application.engine_name
    # Set up index configuration and mapping
    #
    settings index: {number_of_shards: 1, number_of_replicas: 0} do
      mapping do
        indexes :title, type: 'multi_field' do
          indexes :title, analyzer: 'snowball'
          indexes :tokenized, analyzer: 'simple'
        end

        indexes :desc, type: 'multi_field' do
          indexes :desc, analyzer: 'snowball'
          indexes :tokenized, analyzer: 'simple'
        end

        indexes :created_at, type: 'date'
        indexes :price
        indexes :image

        indexes :categories do
          indexes :id
          indexes :name
        end

        indexes :location do
          indexes :id
          indexes :name
        end
      end
    end
    after_touch() { __elasticsearch__.index_document }

    def as_indexed_json(options = {})
      hash = self.as_json(
          include: {categories: {only: [:id, :name]},
                    location: {only: [:id, :name]}
          })
      hash
    end

    def self.search(query, options={})

      __set_filters = lambda do |key, f|

        @search_definition[:filter][:and] ||= []
        @search_definition[:filter][:and] |= [f]

        @search_definition[:facets][key.to_sym][:facet_filter][:and] ||= []
        @search_definition[:facets][key.to_sym][:facet_filter][:and] |= [f]
      end

      @search_definition = {
          query: {},
          filter: {},
          facets: {
              categories: {
                  terms: {
                      field: 'categories.name'
                  },
                  facet_filter: {}
              },
              location: {
                  terms: {
                      field: 'location.name'
                  },
                  facet_filter: {}
              }
          }
      }


      if options[:category]
        f = {terms: { "categories.name" => options[:category].split(',')}}

        __set_filters.(:location, f)

      end

      if options[:location]
        f = {terms: { "location.name" => options[:location].split(',')}}

        __set_filters.(:categories, f)
      end


      unless query.blank?
        @search_definition[:query] = {
            bool: {
                should: [
                    {
                    	multi_match: {
                        	query: query,
                        	fields: ['title^10', 'desc^2'],
                        	operator: 'and'
                    	}
                    }
                ]
            }
        }
      else
        @search_definition[:query] = {match_all: {}}
        #@search_definition[:sort]  = { published_on: 'desc' }
      end
      #puts @search_definition
      __elasticsearch__.search(@search_definition)
    end

  end
end

```

Now update the ```app/models/post.rb``` file.

```ruby
class Post < ActiveRecord::Base
  include Searchable
  ..........
  ..........
end
```

now update the **index** controller action of **Post**. update ```app/controllers/posts_controller.rb``` file

```ruby
  def index
    options = {
        category: params[:category],
        location: params[:locations],
        sort: params[:sort]
    }
    @posts = Post.search(params[:query],options).page(params[:page]).results
  end
```

now we need to index all post to elasticsearch server. run the command on console or make a rake task

```
>> Post.import 
```

now we need to update the ```app/views/index.html.erb``` file

```ruby
<div class="container">
  <div class="row searchbox ">
    <div class="col-md-6 col-md-offset-3">

      <%= form_for posts_path, :method => 'get' do %>
          <div class="input-group">
            <%= text_field_tag :query, params[:query], class: "form-control", placeholder: "Search for..." %>
            <span class="input-group-btn">
            <%= submit_tag "GO!", class: "btn btn-default", name: nil %>
            </span>
          </div>
      <% end %>

    </div>
  </div>

  <div class="row">

    <div class="col-md-3">
      <div class="panel panel-primary">
        <div class="panel-heading">
          <h3 class="panel-title">Categories</h3>
        </div>

        <div class="panel-body category-search">
          <% @posts.response.response['facets']['categories']['terms'].each do |c|  %>
              <div class="checkbox">
                <label>
                  <input type="checkbox" value="<%= c['term'] %>"><%= "#{c['term'].capitalize()}(#{ c['count']})" %>
                </label>
              </div>
          <% end %>
        </div>
      </div>

      <div class="panel panel-success">
        <div class="panel-heading">
          <h3 class="panel-title">Locations</h3>
        </div>

        <div class="panel-body location-search">
          <% @posts.response.response['facets']['location']['terms'].each do |l| %>
              <div class="checkbox">
                <label>
                  <input type="checkbox" value="<%= l['term'] %>"><%= "#{ l['term'].capitalize()}(#{ l['count']})" %>
                </label>
              </div>
          <% end %>
        </div>
      </div>

      <div class="panel panel-info">
        <div class="panel-heading">
          <h3 class="panel-title">Price</h3>
        </div>
        <div class="panel-body">
          Price panel
        </div>
      </div>
    </div>

    <div class="col-md-9 posts-content">
      <%= paginate @posts,:remote => false %>
      <div class="row">
        <% @posts.each do |post| %>
            <%= render partial: 'post',object: post %>
        <% end %>
      </div>
      <%= paginate @posts %>
    </div>
  </div>

</div>
```
Now we need to filter facet data according to the user choice. I did the whole task in coffeescript. I created a file ```search.cofee```  in  ```app/javascripts```

```javascript
getParameters = ->
  query = window.location.search.substring(1)
  raw_vars = query.split("&")
  params = {}

  for v in raw_vars
    [key,val] = v.split("=")
    params[key] = decodeURIComponent(val)
  console.log(params)
  params

checkFilters = (selector,filters) ->
  $(selector).each ->
    for filter in filters
      $(selector).find("input:checkbox[value='" + filter + "']").attr("checked",true)

#$(document).on 'ready', ->
ready = ->
  filters = {
    'categories': [],
    'locations': []
  }

  parameters = getParameters()
  console.log('caeded')
  if parameters.category?
    for category in parameters.category.split(',')
      filters.categories.push(category)
  if parameters.locations?
    for location in parameters.locations.split(',')
      filters.locations.push(location)

  #check box
  checkFilters('.category-search',filters.categories)
  checkFilters('.location-search',filters.locations)

  #set sort
  query = parameters.query
  if (!query)
    sort_by = 'recent'
  else
    sort_by = 'relevance'

  para_sort = parameters.sort_by
  if !!para_sort
    sort_by = para_sort
  $('#sort_by').val(sort_by)

  # Checking and unchecking filter boxes for industry
  $('.category-search [type="checkbox"]').on 'click', ->
    value = $(this).val()
    if $(this).is(':checked')
      filters.categories.push(value)
    else
      index = filters.categories.indexOf(value)
      filters.categories.splice(index, 1) if index > -1
    filterSearch(filters)

  # Checking and unchecking filter boxes for location
  $('.location-search [type="checkbox"]').on 'click', ->
    value = $(this).val()
    if $(this).is(':checked')
      filters.locations.push(value)
    else
      index = filters.locations.indexOf(value)
      filters.locations.splice(index, 1) if index > -1
    filterSearch(filters)

  #  $('#sort_by').on 'change', ->
  #    filterSearch(filters)

  filterSearch = (filters = undefined) ->
    complete_url = document.URL
    full = complete_url.substring(0, complete_url.indexOf('?'));#// location.protocol+'//'+location.hostname+(location.port ? ':'+location.port: '');
    query = getParameters().query
    if !query?
      query = ""
    url = full+"?query=" + query

    #console.log(filters.categories)

    if filters?
      if filters.categories.length > 0
        url = url + '&category=' + encodeURIComponent(filters.categories.join(','))
      if filters.locations.length > 0
        url = url + '&locations=' + encodeURIComponent(filters.locations.join(','))

    #sort_by = $('#sort_by').val()
    #if sort_by.length > 0
    #url = url + "&sort_by=" + sort_by

    window.location.href = url

$(document).ready(ready)
$(document).on('page:load',ready)
```

now cheers!!

you can find the whole project in [Github](https://github.com/farhan-faruque/RailsPostSearch) 

