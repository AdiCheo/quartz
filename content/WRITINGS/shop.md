---
title: "Shop"
alias: "shop"
feature_image: "nan"
type: "post"
status: "draft"
draft: true
visibility: "public"
modified: "2022-05-23T05:31:05.000Z"
---

<p></p><!--kg-card-begin: html--><link rel="preconnect" href="https://app.snipcart.com">
<link rel="preconnect" href="https://cdn.snipcart.com">
<link rel="stylesheet" href="https://cdn.snipcart.com/themes/v3.0.31/default/snipcart.css" />
<script async src="https://cdn.snipcart.com/themes/v3.0.31/default/snipcart.js"></script>
<div hidden id="snipcart" data-api-key="OTM2OGJhNDEtMmM0Zi00OWRhLWI1MzEtNjdhNzE0ZjdiMmNiNjM3NTA4MzcyMDA3MTkwMTgz" data-config-modal-style="side"></div>
<!--kg-card-end: html-->
<figure class="kg-card kg-bookmark-card"><a class="kg-bookmark-container" href="__GHOST_URL__/posts/joyful-nowhere/"><div class="kg-bookmark-content"><div class="kg-bookmark-title">Joyful NowHere</div><div class="kg-bookmark-description">An all inclusive training retreat to escape any limitations and live a location independent and financially secure life.</div><div class="kg-bookmark-metadata">
<a class="kg-bookmark-icon" src="https://adicheo.com/favicon.png" alt=""><span class="kg-bookmark-author">ADICHEO</span><span class="kg-bookmark-publisher">Adi K O</span></div></div><div class="kg-bookmark-thumbnail">
<a src="https://images.unsplash.com/photo-1490730141103-6cac27aaab94?crop&#x3D;entropy&amp;cs&#x3D;tinysrgb&amp;fit&#x3D;max&amp;fm&#x3D;jpg&amp;ixid&#x3D;MXwxMTc3M3wwfDF8c2VhcmNofDJ8fEpveXxlbnwwfHx8&amp;ixlib&#x3D;rb-1.2.1&amp;q&#x3D;80&amp;w&#x3D;2000" alt=""></div></a>
</figure><!--kg-card-begin: html--><button class="snipcart-add-item"
  data-item-id="joyful-nowhere"
  data-item-price="5999.99"
  data-item-url="/posts/joyful-nowhere"
  data-item-description="A fully inclusive travel, adventure, and freedom experience."
  data-item-image="https://images.unsplash.com/photo-1490730141103-6cac27aaab94?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDJ8fEpveXxlbnwwfHx8&ixlib=rb-1.2.1&q=80&w=2000"
  data-item-name="Joyful NowHere">
  Add to cart
</button><!--kg-card-end: html--><!--kg-card-begin: html--><style>
@import url(https://fonts.googleapis.com/css?family=Raleway:400,700);

$dark:#000;
$gold:#D4AF37;

//======= breakpoints
$tablet:40rem;

@mixin tablet {
  @media (max-width: #{$tablet}) {
    @content;
  }
}


// reset
*, *:before, *:after {
  margin:0;
  padding:0;
  box-sizing:border-box;
}


// global
html, body {
  width:100%;
  height:100%;
}

body {
  font-family: 'Raleway', sans-serif;
  line-height:160%;
  font-size:100%;
}


// this wraps the gallery
.fullwidth {
  width:100%;
  padding-top:4rem;
  background-color:lighten($dark, 85%);
}


// centering the items 
.gallery {
  width:100%;
  max-width:60rem;
  margin-right:auto;
  margin-left:auto;
  padding-right:2rem;
  padding-bottom:4rem;
  padding-left:2rem;
}

// each item in gallery
.gallery .item {
  width:100%;
  padding-top:2rem;
  padding-bottom:2rem;
  display:flex;
  flex-direction:row;
  justify-content:flex-start;
  align-items:center;
  flex-wrap:wrap; 
  
  // switch to vertical order and 
  // add spacing between items 
  // at given breakpoint
  @include tablet {
    padding-top:4rem;
    padding-bottom:4rem;
    flex-direction:column;
    text-align:center;
  }
  
  // every second item is aligned right
  &:nth-child(even) {justify-content:flex-end;}
  
  // change the order from image and caption
  &:nth-child(even) .img-wrap {
    order:2;
    // reset to normal order at given breakpoint
    @include tablet {order:0;}
  }
  
  // change the order from image and caption
  &:nth-child(even) caption {
    order:1;
    // reset to normal order at given breakpoint
    @include tablet {order:0;}
  }
}

// to use pseudo elements I need an additional element
// because images can't have pseudo elements
.gallery .item .img-wrap {
  position:relative;
  padding:0.8rem;
  width:50%;
  flex-basis:50%;
  border-radius:50%;
  
  @include tablet {
    width:80%;
    flex-basis:80%;
  }
  
  // the pseudo elements are just decoration
  // given the natural z-index order, the ":after" will cover the ":before"
  &:before, &:after {
    content:'';
    position:absolute;
    border-radius:50%;
    transform:rotate(-90deg);
  }
  &:before {
    top:1px;
    right:1px;
    bottom:1px;
    left:1px;
    border-top:1px solid $gold;
    border-right:1px solid transparent;
    border-bottom:1px solid $gold;
    border-left:1px solid transparent;
  }
  &:after {
    top:0;
    right:0;
    bottom:0;
    left:0;
    border-top:3px solid lighten($dark, 85%);
    border-right:3px solid transparent;
    border-bottom:3px solid lighten($dark, 85%);
    border-left:3px solid transparent;
    transition:transform 0.5s;
  } 
  
  img {
    display:block;
    width:100%;
    height:auto;
    padding:1.5rem;
    border-radius:50%;
    background-color:lighten($dark, 90%);
    background-image:radial-gradient(lighten($dark, 90%), lighten($dark, 80%) 80%);
    background-size:130% 130%;
    background-position:0 0;
    background-repeat:no-repeat;
    box-shadow:
      inset 2px 2px 5px lighten($dark, 70%),
      2px 2px 15px lighten($dark, 90%),
      inset 15px 15px 50px rgba($dark, 0.1);
  }
}

// when hovering one item one pseudo element on the .img-wrap will move
.gallery .item:hover .img-wrap:after {transform:rotate(0deg);}


// to make this layout more dynamic, the item will grow and shrink in size from beginning to end
// like "30 - 40 - 50 - 40 - 30"
.gallery .item:nth-child(1) .img-wrap,
.gallery .item:nth-child(5) .img-wrap {
  width:30%;
  flex-basis:30%;
  
  @include tablet {
    width:60%;
    flex-basis:60%;
  }
}

.gallery .item:nth-child(2) .img-wrap,
.gallery .item:nth-child(4) .img-wrap {
  width:40%;
  flex-basis:40%;
  
  @include tablet {
    width:70%;
    flex-basis:70%;
  }
}


// the caption for each item
.gallery .item .caption {
  padding-right:1rem;
  padding-left:1rem;
  position:relative;
  color:lighten($dark, 60%);
  
  // add some spacing at given breakpoint
  @include tablet {padding-top:1rem;}
  
  h3 {
    position:relative;
    margin-bottom:1rem;
    font-weight:400;
    font-size:1rem;
    text-transform:uppercase;
    letter-spacing:1px;
  }
  
  a {
    display:inline-block;
    position:relative;
    padding:0.3rem 1rem;
    color:inherit;
    text-decoration:none;
    border:1px solid lighten($dark, 70%);
    border-radius:3px;
  }
  
  .btn-buy {
    margin-right:1rem;
    color:$gold;
    border:1px solid $gold;
    letter-spacing:1px;
  }
}

</style>

<div class="fullwidth">
  
  <div class="gallery">
    
    
<figure class="item">
      <div class="img-wrap">
<a src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/46992/cl-01.png" alt="" /></div>
      <figcaption class="caption">
          <h3>Luminor Marina 1950<br/>3 days automatic ACCIAIO</h3>
          <a class="btn-buy" href="#">Buy</a>
          <a class="btn-details" href="#">See details</a>
      </figcaption>
    
</figure>
    
    
<figure class="item">
      <div class="img-wrap">
<a src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/46992/cl-02.png" alt="" /></div>
      <figcaption class="caption">
          <h3>Radiomir 1940 Acciaio</h3>
          <a class="btn-buy" href="#">Buy</a>
          <a class="btn-details" href="#">See details</a>
      </figcaption>
    
</figure>
    
    
<figure class="item">
      <div class="img-wrap">
<a src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/46992/cl-03.png" alt="" /></div>
      <figcaption class="caption">
          <h3>L'egiziano</h3>
          <a class="btn-buy" href="#">Buy</a>
          <a class="btn-details" href="#">See details</a>
      </figcaption>
    
</figure>
    
    
<figure class="item">
      <div class="img-wrap">
<a src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/46992/cl-04.png" alt="" /></div>
      <figcaption class="caption">
          <h3>Luminor Chrono 2000</h3>
          <a class="btn-buy" href="#">Buy</a>
          <a class="btn-details" href="#">See details</a>
      </figcaption>
    
</figure>
    
    
<figure class="item">
      <div class="img-wrap">
<a src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/46992/cl-05.png" alt="" /></div>
      <figcaption class="caption">
          <h3>Radiomir 1940<br/>Chronograph Oro Rosso</h3>
          <a class="btn-buy" href="#">Buy</a>
          <a class="btn-details" href="#">See details</a>
      </figcaption>
    
</figure>
    
  </div>
  
</div>
<!--kg-card-end: html-->
