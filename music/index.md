---
title: Music
author: Nat
layout: one-column
---
<div id="lyrics-list">
  <h2>
    Songs
  </h2>
  
  <p>
    Including lyrics, chords, sheet music, and links to albums and videos.
  </p>
  
  <ul class="page-list subpages-page-list ">
  {% for otherpage in site.pages %}
    {% if otherpage.layout == 'lyrics' %}
      <li class="page_item">
        <a href="{{ otherpage.url }}">{{ otherpage.title }}</a>
      </li>
    {% endif %}
  {% endfor %}
  </ul>
</div>

<div id="albums">
  <h2>Albums</h2>
  
  <p>
    <a href="http://strangerways.bandcamp.com/album/guilt-angst-fairy-tales" class="album"><img src="/images/GAFT-cover-final-112x112.jpg" alt="" title="Guilt, Angst &amp; Fairy Tales Cover" width="112" height="112" class="size-thumbnail wp-image-176" /><br /><br /><strong>Guilt, Angst &amp; Fairy Tales</strong><br /><i>2012</i></a>
    <a href="http://strangerways.bandcamp.com/album/strangers-at-the-gate" class="album"><img class="size-thumbnail wp-image-76" title="Strangers at the Gate Cover" src="/images/Stranger-Ways-CD-Cover-150x150.jpg" alt="" width="112" height="112" /><br /><br /><strong>Strangers at the Gate</strong><br /><i>2011</i></a>
  </p>
  
  <h2>Demos</h2>
  
  <p>We have some unpublished demo recordings you can listen to if you like.  They're <a href="http://strangerways.bandcamp.com/album/unpublished-demos">up on Bandcamp</a>.</p>
</div>
