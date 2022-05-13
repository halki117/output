jyun-en-master/web/app/themes/jyun-en/footer-enkiri.php
```

--------------------------ここから
<div class="p-enkiri-pickup__bottom">
    <a href="#" class="c-arrow--top p-enkiri-pickup__arrow">
      <img src="<?php echo get_template_directory_uri(); ?>/assets/img/pagetop-arrow.svg" alt="ページトップ">
      <!-- <span></span> -->
    </a>
</div>
<section class="l-enkiri-section p-enkiri-bottom">
  <form class="w-100" action="<?php host_domain_getter() ?>/search-result" method="GET">
    <div class="p-enkiri-bottom__search">
      <p class="p-index-links__search-img">
        <button class="btn-none d-flex">
          <img src="<?php echo get_template_directory_uri(); ?>/assets/img/search_icon.svg" alt="">
        </button>
      </p>
      <input class="top-footer-search m-0" type="text" placeholder="サイト内フリーワード検索" name="search">
    </div>
  </form>
  <div class="p-enkiri-bottom__item-wrapper">
    <!-- <a href="#" class="p-enkiri-bottom__item">
      <p class="p-enkiri-bottom__item-img c-img--outer">
        <img src="<?php echo get_template_directory_uri(); ?>/assets/img/mizubiki02.png" alt="水引きの画像">
      </p>
      <p class="p-enkiri-bottom__item-text">ご祈祷・お祓いなどのご予約はこちら</p>
    </a> -->
    <a href="/tostaff/" class="p-enkiri-bottom__item">
      <p class="p-enkiri-bottom__item-img">
        <img src="<?php echo get_template_directory_uri(); ?>/assets/img/torii.png" alt="鳥居の画像" class="p-enkiri-bottom__item-img">
      </p>
      <p class="p-enkiri-bottom__item-text">
        寺社等の施設関係者の方はこちら
      </p>
    </a>
  </div>
  <p class="p-enkiri-bottom__cloud-right">
    <img src="<?php echo get_template_directory_uri(); ?>/assets/img/enkiri/enkiri-cloud-bottom02.png" alt="雲の画像" class="c-img">
  </p>
</section>

----------------------ここまで

<footer class="l-enkiri-footer">
```




jyun-en-master/web/app/themes/jyun-en/header.php
```
  <link rel="stylesheet" href="https://unpkg.com/swiper/swiper-bundle.min.css" />
  
----------------------ここから

  <?php if(is_page('single') && array_search('縁結び', (array)get_field('ご利益')) === false){ ?>
    <link rel="stylesheet" type="text/css" href="<?php echo get_template_directory_uri(); ?>/assets/css/enkiri.css">
  <?php } ?>
----------------------ここまで

  <!-- JS -->
  <script src="https://unpkg.com/swiper/swiper-bundle.min.js"></script>

```


jyun-en-master/web/app/themes/jyun-en/single-temple.php
jyun-en-master/web/app/themes/jyun-en/single-shrine.php
```
ページ最下部

<?php if(array_search('縁結び', (array)get_field('ご利益')) === false){ ?>
  <?php get_template_part('footer', 'enkiri'); ?>
<?php }else{ ?>
  <?php get_footer(); ?>
<?php } ?>

```
