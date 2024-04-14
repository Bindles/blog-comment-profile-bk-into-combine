<!-- app/views/posts/show.html.erb -->
<div id="<%= dom_id post %>">
<%= link_to "Show this post", post, class: 'btn btn-outline-warning' %>

  <p>
    <strong>Title:</strong>
    <%= post.title %>
  </p>

  <p>
    <strong>Content:</strong>
    <%= post.content %>
  </p>

  <p>
    <strong>User:</strong>
    <%#= post.user_id %>
    <%#= User.find(1).email %>
    <%#= User.find(post.user_id).email %>
    <%= @current_user %><br>

    <%#= post.comments.inspect%><br>

    <%#= @comments.inspect%><br><br>

    <%# post.comments.each do |ins|%>
      <%#= ins.inspect %><br>
    <%# end %>

    <%= render 'debcomment' %>
  </p>


<!-- Render existing comments -->
<h2>Comments</h2>

<% if controller_name == 'posts' && action_name == 'show' %>
  <%#= params.inspect %><br>
  <%#= params[:id] %><br>
  <%#= post.comments.find_by(commentable_id: params[:id]).content %>
  <% if @comments.length <= 2 %>
    <% @comments.each do |comment| %>
    <br>
      <%= comment.content %> 
    <% end %>
  <% else %>
    <div id="showComments">
      <% @comments.first(2).each do |comment| %>
      <br>
        <%= comment.content %>
      <% end %>
    </div>
    <button id="showMore">Show More</button>

    <script>
      document.getElementById('showMore').addEventListener('click', function() {
        var commentsDiv = document.getElementById('showComments');
        <% @comments.drop(2).each do |comment| %>
          var newComment = document.createElement('div');
          newComment.innerHTML = '<%= j comment.content %>';
          commentsDiv.appendChild(newComment);
        <% end %>
        this.style.display = 'none'; // Hide the "Show More" button
      });
    </script>
  <% end %>

<%#= link_to "Show this post", post(@comment, view_comments: 0), class: 'btn btn-outline-warning' %>
<%#= link_to 'Hide Comments', root_path(@comment, view_comments: 0) unless @view_comments.zero? %>
<%#= link_to 'Show Comments', root_path(@comment, view_comments: 1) if @view_comments.zero? %>
<%= link_to 'Hide Comments', post_path(@post, view_comments: 0) unless @view_comments.zero? %>
<%= link_to 'Show Comments', post_path(@post, view_comments: 1) if @view_comments.zero? %>

<% if @view_comments.nonzero? %>
  <!-- Render comments -->
  <% @post.comments.each do |comment| %>
    <!-- Render comment details -->
  <% end %>
<% end %>

  <% if @view_comments.nonzero? %>

    <% @comments.each do |comment| %>
    <ul>
      <% comment.attributes.each do |attribute, value| %>
        <li><strong><%= attribute %>:</strong> <%= value %></li>
      <% end %>
    </ul>
    <% end %>
  <% end%>


    <% @comments.each do |comment| %>
    <br>
      <%= comment.content %>
    <% end %>

  <%= render 'comments/cform', commentable: @post %>
<% end %>



  <%# <%= render 'comments/cform', commentable: @post %> %>

</div>
