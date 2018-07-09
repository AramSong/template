# README
javascript 모듈화 도구

https://d2.naver.com/helloworld/0239818

- setInterval() : 일정시간마다 반복 실행하는 함수
- Template
- pusher(채팅방 ,채팅방에 join) 
- 별점

Bootstrap v3.2.0 (http://getbootstrap.com)

Gemfile

    #bootstrap 3
    gem 'bootstrap-sass'
    
    #font-awesome
    gem 'font-awesome-rails'
    #turbolink 삭제
    --------------------------------------------------------------------------------
    rails g controller home index
    --------------------------------------------------------------------------------
    #config/routes.rb
      root 'home#index'
    #app/assets/javascripts/application.js
    //= require turbolinks		삭제
    //= require_tree . 			삭제
    //= require bootstrap		추가
    #app/assets/stylesheets/application.css->application.scss
    #내용 다 삭제 후
    @import 'bootstrap';
    @import 'font-awesome';
    #추가
    --------------------------------------------------------------------------------
    #index.html에서 css만 선택해서 stylesheets/home.scss에 복사
    @import 'font-awesome.min';
    @import 'jquery.tagsinput';
    @import 'owl.carousel';
    @import 'styles';
    @import 'responsive';
    -------------------------------------------------------------------------------
    # html/css 파일에 있는 것(home.scss에 적은 것)을 vendor/stylesheets
    -------------------------------------------------------------------------------
     #views/layouts/application.html.erb
     <head>
        <title>TemplateApp</title>
        <%= csrf_meta_tags %>
    	#viewport 복사
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <%= stylesheet_link_tag    'application', media: 'all' %>
    	#추가
    	<%= stylesheet_link_tag    params[:controller],media: 'all' %>
        <%= javascript_include_tag 'application'%>
      </head>
    --------------------------------------------------------------------------------
        rake assets:precompile
    #public/assets 에서 확인해보면 compile된 파일들을 확인할 수 있다.
    rake assets:clobber	#public assets 폴더 삭제
    
    



#config/initializer/assets.rb

    #config/initializer/assets.rb
    # Be sure to restart your server when you modify this file.
    
    # Version of your assets, change this if you want to expire all your assets.
    Rails.application.config.assets.version = '1.0'
    
    # Add additional assets to the asset load path
    # Rails.application.config.assets.paths << Emoji.images_path
    
    # Precompile additional assets.
    # application.js, application.css, and all non-JS/CSS in app/assets folder are already added.
    Rails.application.config.assets.precompile += %w( home.js 
                                                      home.scss)
    
    # home.coffee파일을 home.js로 변경

- rake:precomplie 후 rake aborted 된 부분에  오류난 부분이 어디인지 알 수 있다. 
- header/body/footer
  views/shared폴더 생성
      # _nav.html.erb
      <header id="header">
      	<div class="header-top-bar"> =
                  ...
      </header> 복사.
      # _footer.html.erb
      <footer id = "footer"></footer> 복사.
  

application.html.erb

    <!DOCTYPE html>
    <html>
      <head>
        <title>TemplateApp</title>
        <%= csrf_meta_tags %>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <%= stylesheet_link_tag    'application', media: 'all' %>
        <%= stylesheet_link_tag    params[:controller], media: 'all' %>
        <%= javascript_include_tag 'application' %>
      </head>
    
      <body>
       <div id="main-wrapper" class="our-agents-content"> 
          <%= render 'shared/nav' %>
          <%= yield %>
          <%= render 'shared/footer' %>
          <%= yield 'javascript_content' %>
       </div>
      </body>
    </html>

index.html.erb

    #맨 끝에 추가
    <% content_for 'javascript_content' do %>
    <%= javascript_include_tag params[:controller] %>
    <script>
        console.log("content_for");
    </script>
    <% end %>

- yield 는 기본적으로 현재 cotroller의 action erb파일을 찾아감.
- 지정해놓을 경우엔 content_for로 한 블럭을 지정해놓을 수 있다.
- yield 위치명, content_for 위치명

home.js

    //=require jquery.ba-outside-events.min
    //=require jquery.responsive-tabs
    //=require jquery.flexslider-min
    //=require jquery.fitvids
    //=require jquery-ui-1.10.4.custom.min
    //=require jquery.inview.min
    //=require jquery-ui-1.10.4.custom.min
    //=require carousel.min
    //=require scripts
    
    #vendor/assets/javascripts 폴더에 해당파일 복사 

- 이미지 => app/assets/images 에 저장 

    '../img/ ...' => <%= asset-path 로 수정 >



- font  => public/assets/fonts 생성 폰트 저장
