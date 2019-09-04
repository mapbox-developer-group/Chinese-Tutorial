





<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
  <link rel="dns-prefetch" href="https://github.githubassets.com">
  <link rel="dns-prefetch" href="https://avatars0.githubusercontent.com">
  <link rel="dns-prefetch" href="https://avatars1.githubusercontent.com">
  <link rel="dns-prefetch" href="https://avatars2.githubusercontent.com">
  <link rel="dns-prefetch" href="https://avatars3.githubusercontent.com">
  <link rel="dns-prefetch" href="https://github-cloud.s3.amazonaws.com">
  <link rel="dns-prefetch" href="https://user-images.githubusercontent.com/">



  <link crossorigin="anonymous" media="all" integrity="sha512-aVn2DoCuXdXX9G3sp/Luupl/Ui00/iXrUh7Ke3geLlkigQY8GHBky7kKRSuyeKxGApWDdCQUy+6gTF1ZmYHWkw==" rel="stylesheet" href="https://github.githubassets.com/assets/frameworks-6b8b7859c4b8fbe3ab45f8ab0905a9f8.css" />
  
    <link crossorigin="anonymous" media="all" integrity="sha512-sLO1JuwvgYFNw548DR/keEd4Blx2a4qLD++xhOua+7VKNkB16DtOt9LOFNQjahAnCxt76u9Vh2vlD94gzan2/Q==" rel="stylesheet" href="https://github.githubassets.com/assets/github-8574c5af92bd7369457853930ff4eb9d.css" />
    
    
    
    

  <meta name="viewport" content="width=device-width">
  
  <title>help/building-a-store-locator.md at publisher-production · mapbox/help</title>
    <meta name="description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub.">
    <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
  <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
  <meta property="fb:app_id" content="1401488693436528">

    <meta name="twitter:image:src" content="https://avatars2.githubusercontent.com/u/600935?s=400&amp;v=4" /><meta name="twitter:site" content="@github" /><meta name="twitter:card" content="summary" /><meta name="twitter:title" content="mapbox/help" /><meta name="twitter:description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub." />
    <meta property="og:image" content="https://avatars2.githubusercontent.com/u/600935?s=400&amp;v=4" /><meta property="og:site_name" content="GitHub" /><meta property="og:type" content="object" /><meta property="og:title" content="mapbox/help" /><meta property="og:url" content="https://github.com/mapbox/help" /><meta property="og:description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub." />

  <link rel="assets" href="https://github.githubassets.com/">
  <link rel="web-socket" href="wss://live.github.com/_sockets/VjI6MzAyOTU4NTE3OmE5YjdmYzhjNzgzZGQxMDIwYmQ2YjRhZjlkN2QzZWIzODU1YmQ5YmQ3ODI4ZjA2ZGYxZjZiN2FkYmEyMGFlMjc=--8e4880d6869dc96038666a1bae5227f5538aece5">
  <meta name="pjax-timeout" content="1000">
  <link rel="sudo-modal" href="/sessions/sudo_modal">
  <meta name="request-id" content="CDFB:9475:9E852:EFEEE:5D701D80" data-pjax-transient>


  <link rel="sso-modal" href="/orgs/mapbox/sso_modal" data-pjax-transient="true"></link><link rel="sso-session" href="/orgs/mapbox/sso_status.json" data-pjax-transient="true"></link><meta name="sso-expires-around" content="1567704602" data-pjax-transient="true"></meta>

  <meta name="selected-link" value="repo_source" data-pjax-transient>

      <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
    <meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-site-verification" content="GXs5KoUUkNCoaAZn7wPN-t01Pywp9M3sEjnt_3_ZWPc">

  <meta name="octolytics-host" content="collector.githubapp.com" /><meta name="octolytics-app-id" content="github" /><meta name="octolytics-event-url" content="https://collector.githubapp.com/github-external/browser_event" /><meta name="octolytics-dimension-request_id" content="CDFB:9475:9E852:EFEEE:5D701D80" /><meta name="octolytics-dimension-region_edge" content="sea" /><meta name="octolytics-dimension-region_render" content="iad" /><meta name="octolytics-dimension-ga_id" content="" class="js-octo-ga-id" /><meta name="octolytics-dimension-visitor_id" content="2058165157458336909" /><meta name="octolytics-actor-id" content="18397640" /><meta name="octolytics-actor-login" content="Jing-flyloveyin" /><meta name="octolytics-actor-hash" content="c7be0e1b8bc813e56ceee222f4a1c9e2890774570591d5891573b62c21660107" />
<meta name="analytics-location" content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" />



    <meta name="google-analytics" content="UA-3769691-2">

  <meta class="js-ga-set" name="userId" content="a377d279e504cd9111bf6c4e502c8d97">

<meta class="js-ga-set" name="dimension1" content="Logged In">



  

      <meta name="hostname" content="github.com">
    <meta name="user-login" content="Jing-flyloveyin">

      <meta name="expected-hostname" content="github.com">
    <meta name="js-proxy-site-detection-payload" content="NGYwNzI5NTM1OGJlNjhmZTMyYmYzZWY1NWMyNTFhOGVhNzU0ZTYxYzU1NWU5ZTNkNTc1YTc1OGM1NDkxZjFlMHx7InJlbW90ZV9hZGRyZXNzIjoiNDUuNzkuODMuODEiLCJyZXF1ZXN0X2lkIjoiQ0RGQjo5NDc1OjlFODUyOkVGRUVFOjVENzAxRDgwIiwidGltZXN0YW1wIjoxNTY3NjI4Njc4LCJob3N0IjoiZ2l0aHViLmNvbSJ9">

    <meta name="enabled-features" content="ACTIONS_V2_ON_MARKETPLACE,MARKETPLACE_FEATURED_BLOG_POSTS,MARKETPLACE_INVOICED_BILLING,MARKETPLACE_SOCIAL_PROOF_CUSTOMERS,MARKETPLACE_TRENDING_SOCIAL_PROOF,MARKETPLACE_RECOMMENDATIONS,MARKETPLACE_PENDING_INSTALLATIONS,NOTIFY_ON_BLOCK,RELATED_ISSUES,GHE_CLOUD_TRIAL">

  <meta name="html-safe-nonce" content="fb97dd135de80342fdc477688b418fc612fd0e7e">

  <meta http-equiv="x-pjax-version" content="785dc78f1f1353014e3eece9d3f39215">
  

      <link href="https://github.com/mapbox/help/commits/publisher-production.atom?token=AEMLTSEBVEOCCWWCQTM75253PVPBM" rel="alternate" title="Recent Commits to help:publisher-production" type="application/atom+xml">

  <meta name="go-import" content="github.com/mapbox/help git https://github.com/mapbox/help.git">

  <meta name="octolytics-dimension-user_id" content="600935" /><meta name="octolytics-dimension-user_login" content="mapbox" /><meta name="octolytics-dimension-repository_id" content="34758294" /><meta name="octolytics-dimension-repository_nwo" content="mapbox/help" /><meta name="octolytics-dimension-repository_public" content="false" /><meta name="octolytics-dimension-repository_is_fork" content="false" /><meta name="octolytics-dimension-repository_network_root_id" content="34758294" /><meta name="octolytics-dimension-repository_network_root_nwo" content="mapbox/help" /><meta name="octolytics-dimension-repository_explore_github_marketplace_ci_cta_shown" content="false" />


    <link rel="canonical" href="https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/building-a-store-locator.md" data-pjax-transient>


  <meta name="browser-stats-url" content="https://api.github.com/_private/browser/stats">

  <meta name="browser-errors-url" content="https://api.github.com/_private/browser/errors">

  <link rel="mask-icon" href="https://github.githubassets.com/pinned-octocat.svg" color="#000000">
  <link rel="icon" type="image/x-icon" class="js-site-favicon" href="https://github.githubassets.com/favicon.ico">

<meta name="theme-color" content="#1e2327">



  <meta name="webauthn-auth-enabled" content="true">

  <meta name="webauthn-registration-enabled" content="true">

  <link rel="manifest" href="/manifest.json" crossOrigin="use-credentials">

  </head>

  <body class="logged-in env-production emoji-size-boost page-responsive page-blob">
    

  <div class="position-relative js-header-wrapper ">
    <a href="#start-of-content" tabindex="1" class="p-3 bg-blue text-white show-on-focus js-skip-to-content">Skip to content</a>
    <div id="js-pjax-loader-bar" class="pjax-loader-bar"><div class="progress"></div></div>

    
    
    


          <header class="Header js-details-container Details flex-wrap flex-lg-nowrap p-responsive" role="banner">

    <div class="Header-item d-none d-lg-flex">
      <a class="Header-link" href="https://github.com/" data-hotkey="g d" aria-label="Homepage" data-ga-click="Header, go to dashboard, icon:logo">
  <svg class="octicon octicon-mark-github v-align-middle" height="32" viewBox="0 0 16 16" version="1.1" width="32" aria-hidden="true"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
</a>

    </div>

    <div class="Header-item d-lg-none">
      <button class="Header-link btn-link js-details-target" type="button" aria-label="Toggle navigation" aria-expanded="false">
        <svg height="24" class="octicon octicon-three-bars" viewBox="0 0 12 16" version="1.1" width="18" aria-hidden="true"><path fill-rule="evenodd" d="M11.41 9H.59C0 9 0 8.59 0 8c0-.59 0-1 .59-1H11.4c.59 0 .59.41.59 1 0 .59 0 1-.59 1h.01zm0-4H.59C0 5 0 4.59 0 4c0-.59 0-1 .59-1H11.4c.59 0 .59.41.59 1 0 .59 0 1-.59 1h.01zM.59 11H11.4c.59 0 .59.41.59 1 0 .59 0 1-.59 1H.59C0 13 0 12.59 0 12c0-.59 0-1 .59-1z"/></svg>
      </button>
    </div>

    <div class="Header-item Header-item--full flex-column flex-lg-row width-full flex-order-2 flex-lg-order-none mr-0 mr-lg-3 mt-3 mt-lg-0 Details-content--hidden">
        <div class="header-search flex-self-stretch flex-lg-self-auto mr-0 mr-lg-3 mb-3 mb-lg-0 scoped-search site-scoped-search js-site-search position-relative js-jump-to"
  role="combobox"
  aria-owns="jump-to-results"
  aria-label="Search or jump to"
  aria-haspopup="listbox"
  aria-expanded="false"
>
  <div class="position-relative">
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="js-site-search-form" role="search" aria-label="Site" data-scope-type="Repository" data-scope-id="34758294" data-scoped-search-url="/mapbox/help/search" data-unscoped-search-url="/search" action="/mapbox/help/search" accept-charset="UTF-8" method="get"><input name="utf8" type="hidden" value="&#x2713;" />
      <label class="form-control input-sm header-search-wrapper p-0 header-search-wrapper-jump-to position-relative d-flex flex-justify-between flex-items-center js-chromeless-input-container">
        <input type="text"
          class="form-control input-sm header-search-input jump-to-field js-jump-to-field js-site-search-focus js-site-search-field is-clearable"
          data-hotkey="s,/"
          name="q"
          value=""
          placeholder="Search or jump to…"
          data-unscoped-placeholder="Search or jump to…"
          data-scoped-placeholder="Search or jump to…"
          autocapitalize="off"
          aria-autocomplete="list"
          aria-controls="jump-to-results"
          aria-label="Search or jump to…"
          data-jump-to-suggestions-path="/_graphql/GetSuggestedNavigationDestinations#csrf-token=VKtdv0/OjEGroKOMUUeXc6x4GeQNsSTWpJy2mVC7rDHVAoDfFye/mtuFmf83ZKFD8ho/g3GqQ57ob+xpedQCFw=="
          spellcheck="false"
          autocomplete="off"
          >
          <input type="hidden" class="js-site-search-type-field" name="type" >
            <img src="https://github.githubassets.com/images/search-key-slash.svg" alt="" class="mr-2 header-search-key-slash">

            <div class="Box position-absolute overflow-hidden d-none jump-to-suggestions js-jump-to-suggestions-container">
              
<ul class="d-none js-jump-to-suggestions-template-container">
  

<li class="d-flex flex-justify-start flex-items-center p-0 f5 navigation-item js-navigation-item js-jump-to-suggestion" role="option">
  <a tabindex="-1" class="no-underline d-flex flex-auto flex-items-center jump-to-suggestions-path js-jump-to-suggestion-path js-navigation-open p-2" href="">
    <div class="jump-to-octicon js-jump-to-octicon flex-shrink-0 mr-2 text-center d-none">
      <svg height="16" width="16" class="octicon octicon-repo flex-shrink-0 js-jump-to-octicon-repo d-none" title="Repository" aria-label="Repository" viewBox="0 0 12 16" version="1.1" role="img"><path fill-rule="evenodd" d="M4 9H3V8h1v1zm0-3H3v1h1V6zm0-2H3v1h1V4zm0-2H3v1h1V2zm8-1v12c0 .55-.45 1-1 1H6v2l-1.5-1.5L3 16v-2H1c-.55 0-1-.45-1-1V1c0-.55.45-1 1-1h10c.55 0 1 .45 1 1zm-1 10H1v2h2v-1h3v1h5v-2zm0-10H2v9h9V1z"/></svg>
      <svg height="16" width="16" class="octicon octicon-project flex-shrink-0 js-jump-to-octicon-project d-none" title="Project" aria-label="Project" viewBox="0 0 15 16" version="1.1" role="img"><path fill-rule="evenodd" d="M10 12h3V2h-3v10zm-4-2h3V2H6v8zm-4 4h3V2H2v12zm-1 1h13V1H1v14zM14 0H1a1 1 0 0 0-1 1v14a1 1 0 0 0 1 1h13a1 1 0 0 0 1-1V1a1 1 0 0 0-1-1z"/></svg>
      <svg height="16" width="16" class="octicon octicon-search flex-shrink-0 js-jump-to-octicon-search d-none" title="Search" aria-label="Search" viewBox="0 0 16 16" version="1.1" role="img"><path fill-rule="evenodd" d="M15.7 13.3l-3.81-3.83A5.93 5.93 0 0 0 13 6c0-3.31-2.69-6-6-6S1 2.69 1 6s2.69 6 6 6c1.3 0 2.48-.41 3.47-1.11l3.83 3.81c.19.2.45.3.7.3.25 0 .52-.09.7-.3a.996.996 0 0 0 0-1.41v.01zM7 10.7c-2.59 0-4.7-2.11-4.7-4.7 0-2.59 2.11-4.7 4.7-4.7 2.59 0 4.7 2.11 4.7 4.7 0 2.59-2.11 4.7-4.7 4.7z"/></svg>
    </div>

    <img class="avatar mr-2 flex-shrink-0 js-jump-to-suggestion-avatar d-none" alt="" aria-label="Team" src="" width="28" height="28">

    <div class="jump-to-suggestion-name js-jump-to-suggestion-name flex-auto overflow-hidden text-left no-wrap css-truncate css-truncate-target">
    </div>

    <div class="border rounded-1 flex-shrink-0 bg-gray px-1 text-gray-light ml-1 f6 d-none js-jump-to-badge-search">
      <span class="js-jump-to-badge-search-text-default d-none" aria-label="in this repository">
        In this repository
      </span>
      <span class="js-jump-to-badge-search-text-global d-none" aria-label="in all of GitHub">
        All GitHub
      </span>
      <span aria-hidden="true" class="d-inline-block ml-1 v-align-middle">↵</span>
    </div>

    <div aria-hidden="true" class="border rounded-1 flex-shrink-0 bg-gray px-1 text-gray-light ml-1 f6 d-none d-on-nav-focus js-jump-to-badge-jump">
      Jump to
      <span class="d-inline-block ml-1 v-align-middle">↵</span>
    </div>
  </a>
</li>

</ul>

<ul class="d-none js-jump-to-no-results-template-container">
  <li class="d-flex flex-justify-center flex-items-center f5 d-none js-jump-to-suggestion p-2">
    <span class="text-gray">No suggested jump to results</span>
  </li>
</ul>

<ul id="jump-to-results" role="listbox" class="p-0 m-0 js-navigation-container jump-to-suggestions-results-container js-jump-to-suggestions-results-container">
  

<li class="d-flex flex-justify-start flex-items-center p-0 f5 navigation-item js-navigation-item js-jump-to-scoped-search d-none" role="option">
  <a tabindex="-1" class="no-underline d-flex flex-auto flex-items-center jump-to-suggestions-path js-jump-to-suggestion-path js-navigation-open p-2" href="">
    <div class="jump-to-octicon js-jump-to-octicon flex-shrink-0 mr-2 text-center d-none">
      <svg height="16" width="16" class="octicon octicon-repo flex-shrink-0 js-jump-to-octicon-repo d-none" title="Repository" aria-label="Repository" viewBox="0 0 12 16" version="1.1" role="img"><path fill-rule="evenodd" d="M4 9H3V8h1v1zm0-3H3v1h1V6zm0-2H3v1h1V4zm0-2H3v1h1V2zm8-1v12c0 .55-.45 1-1 1H6v2l-1.5-1.5L3 16v-2H1c-.55 0-1-.45-1-1V1c0-.55.45-1 1-1h10c.55 0 1 .45 1 1zm-1 10H1v2h2v-1h3v1h5v-2zm0-10H2v9h9V1z"/></svg>
      <svg height="16" width="16" class="octicon octicon-project flex-shrink-0 js-jump-to-octicon-project d-none" title="Project" aria-label="Project" viewBox="0 0 15 16" version="1.1" role="img"><path fill-rule="evenodd" d="M10 12h3V2h-3v10zm-4-2h3V2H6v8zm-4 4h3V2H2v12zm-1 1h13V1H1v14zM14 0H1a1 1 0 0 0-1 1v14a1 1 0 0 0 1 1h13a1 1 0 0 0 1-1V1a1 1 0 0 0-1-1z"/></svg>
      <svg height="16" width="16" class="octicon octicon-search flex-shrink-0 js-jump-to-octicon-search d-none" title="Search" aria-label="Search" viewBox="0 0 16 16" version="1.1" role="img"><path fill-rule="evenodd" d="M15.7 13.3l-3.81-3.83A5.93 5.93 0 0 0 13 6c0-3.31-2.69-6-6-6S1 2.69 1 6s2.69 6 6 6c1.3 0 2.48-.41 3.47-1.11l3.83 3.81c.19.2.45.3.7.3.25 0 .52-.09.7-.3a.996.996 0 0 0 0-1.41v.01zM7 10.7c-2.59 0-4.7-2.11-4.7-4.7 0-2.59 2.11-4.7 4.7-4.7 2.59 0 4.7 2.11 4.7 4.7 0 2.59-2.11 4.7-4.7 4.7z"/></svg>
    </div>

    <img class="avatar mr-2 flex-shrink-0 js-jump-to-suggestion-avatar d-none" alt="" aria-label="Team" src="" width="28" height="28">

    <div class="jump-to-suggestion-name js-jump-to-suggestion-name flex-auto overflow-hidden text-left no-wrap css-truncate css-truncate-target">
    </div>

    <div class="border rounded-1 flex-shrink-0 bg-gray px-1 text-gray-light ml-1 f6 d-none js-jump-to-badge-search">
      <span class="js-jump-to-badge-search-text-default d-none" aria-label="in this repository">
        In this repository
      </span>
      <span class="js-jump-to-badge-search-text-global d-none" aria-label="in all of GitHub">
        All GitHub
      </span>
      <span aria-hidden="true" class="d-inline-block ml-1 v-align-middle">↵</span>
    </div>

    <div aria-hidden="true" class="border rounded-1 flex-shrink-0 bg-gray px-1 text-gray-light ml-1 f6 d-none d-on-nav-focus js-jump-to-badge-jump">
      Jump to
      <span class="d-inline-block ml-1 v-align-middle">↵</span>
    </div>
  </a>
</li>

  

<li class="d-flex flex-justify-start flex-items-center p-0 f5 navigation-item js-navigation-item js-jump-to-global-search d-none" role="option">
  <a tabindex="-1" class="no-underline d-flex flex-auto flex-items-center jump-to-suggestions-path js-jump-to-suggestion-path js-navigation-open p-2" href="">
    <div class="jump-to-octicon js-jump-to-octicon flex-shrink-0 mr-2 text-center d-none">
      <svg height="16" width="16" class="octicon octicon-repo flex-shrink-0 js-jump-to-octicon-repo d-none" title="Repository" aria-label="Repository" viewBox="0 0 12 16" version="1.1" role="img"><path fill-rule="evenodd" d="M4 9H3V8h1v1zm0-3H3v1h1V6zm0-2H3v1h1V4zm0-2H3v1h1V2zm8-1v12c0 .55-.45 1-1 1H6v2l-1.5-1.5L3 16v-2H1c-.55 0-1-.45-1-1V1c0-.55.45-1 1-1h10c.55 0 1 .45 1 1zm-1 10H1v2h2v-1h3v1h5v-2zm0-10H2v9h9V1z"/></svg>
      <svg height="16" width="16" class="octicon octicon-project flex-shrink-0 js-jump-to-octicon-project d-none" title="Project" aria-label="Project" viewBox="0 0 15 16" version="1.1" role="img"><path fill-rule="evenodd" d="M10 12h3V2h-3v10zm-4-2h3V2H6v8zm-4 4h3V2H2v12zm-1 1h13V1H1v14zM14 0H1a1 1 0 0 0-1 1v14a1 1 0 0 0 1 1h13a1 1 0 0 0 1-1V1a1 1 0 0 0-1-1z"/></svg>
      <svg height="16" width="16" class="octicon octicon-search flex-shrink-0 js-jump-to-octicon-search d-none" title="Search" aria-label="Search" viewBox="0 0 16 16" version="1.1" role="img"><path fill-rule="evenodd" d="M15.7 13.3l-3.81-3.83A5.93 5.93 0 0 0 13 6c0-3.31-2.69-6-6-6S1 2.69 1 6s2.69 6 6 6c1.3 0 2.48-.41 3.47-1.11l3.83 3.81c.19.2.45.3.7.3.25 0 .52-.09.7-.3a.996.996 0 0 0 0-1.41v.01zM7 10.7c-2.59 0-4.7-2.11-4.7-4.7 0-2.59 2.11-4.7 4.7-4.7 2.59 0 4.7 2.11 4.7 4.7 0 2.59-2.11 4.7-4.7 4.7z"/></svg>
    </div>

    <img class="avatar mr-2 flex-shrink-0 js-jump-to-suggestion-avatar d-none" alt="" aria-label="Team" src="" width="28" height="28">

    <div class="jump-to-suggestion-name js-jump-to-suggestion-name flex-auto overflow-hidden text-left no-wrap css-truncate css-truncate-target">
    </div>

    <div class="border rounded-1 flex-shrink-0 bg-gray px-1 text-gray-light ml-1 f6 d-none js-jump-to-badge-search">
      <span class="js-jump-to-badge-search-text-default d-none" aria-label="in this repository">
        In this repository
      </span>
      <span class="js-jump-to-badge-search-text-global d-none" aria-label="in all of GitHub">
        All GitHub
      </span>
      <span aria-hidden="true" class="d-inline-block ml-1 v-align-middle">↵</span>
    </div>

    <div aria-hidden="true" class="border rounded-1 flex-shrink-0 bg-gray px-1 text-gray-light ml-1 f6 d-none d-on-nav-focus js-jump-to-badge-jump">
      Jump to
      <span class="d-inline-block ml-1 v-align-middle">↵</span>
    </div>
  </a>
</li>


    <li class="d-flex flex-justify-center flex-items-center p-0 f5 js-jump-to-suggestion">
      <img src="https://github.githubassets.com/images/spinners/octocat-spinner-128.gif" alt="Octocat Spinner Icon" class="m-2" width="28">
    </li>
</ul>

            </div>
      </label>
</form>  </div>
</div>


      <nav class="d-flex flex-column flex-lg-row flex-self-stretch flex-lg-self-auto" aria-label="Global">
    <a class="Header-link d-block d-lg-none py-2 py-lg-0 border-top border-lg-top-0 border-white-fade-15" data-ga-click="Header, click, Nav menu - item:dashboard:user" aria-label="Dashboard" href="/dashboard">
      Dashboard
</a>
  <a class="js-selected-navigation-item Header-link  mr-0 mr-lg-3 py-2 py-lg-0 border-top border-lg-top-0 border-white-fade-15" data-hotkey="g p" data-ga-click="Header, click, Nav menu - item:pulls context:user" aria-label="Pull requests you created" data-selected-links="/pulls /pulls/assigned /pulls/mentioned /pulls" href="/pulls">
    Pull requests
</a>
  <a class="js-selected-navigation-item Header-link  mr-0 mr-lg-3 py-2 py-lg-0 border-top border-lg-top-0 border-white-fade-15" data-hotkey="g i" data-ga-click="Header, click, Nav menu - item:issues context:user" aria-label="Issues you created" data-selected-links="/issues /issues/assigned /issues/mentioned /issues" href="/issues">
    Issues
</a>
    <div class="mr-0 mr-lg-3 py-2 py-lg-0 border-top border-lg-top-0 border-white-fade-15">
      <a class="js-selected-navigation-item Header-link" data-ga-click="Header, click, Nav menu - item:marketplace context:user" data-octo-click="marketplace_click" data-octo-dimensions="location:nav_bar" data-selected-links=" /marketplace" href="/marketplace">
        Marketplace
</a>      

    </div>

  <a class="js-selected-navigation-item Header-link  mr-0 mr-lg-3 py-2 py-lg-0 border-top border-lg-top-0 border-white-fade-15" data-ga-click="Header, click, Nav menu - item:explore" data-selected-links="/explore /trending /trending/developers /integrations /integrations/feature/code /integrations/feature/collaborate /integrations/feature/ship showcases showcases_search showcases_landing /explore" href="/explore">
    Explore
</a>


    <a class="Header-link d-block d-lg-none mr-0 mr-lg-3 py-2 py-lg-0 border-top border-lg-top-0 border-white-fade-15" href="https://github.com/Jing-flyloveyin">
      <img class="avatar" height="20" width="20" alt="@Jing-flyloveyin" src="https://avatars1.githubusercontent.com/u/18397640?s=60&amp;v=4" />
      Jing-flyloveyin
</a>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form action="/logout" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="ZWCJ1vvze9Ghb4yAsmczQ0zcD6cHRl8YjaDJi2ZjNu4hsrDt6QctZgO0Z+TYF9/NI6djU6SoSttzg6SIfDk6Tg==" />
      <button type="submit" class="Header-link mr-0 mr-lg-3 py-2 py-lg-0 border-top border-lg-top-0 border-white-fade-15 d-lg-none btn-link d-block width-full text-left" data-ga-click="Header, sign out, icon:logout" style="padding-left: 2px;">
        <svg class="octicon octicon-sign-out v-align-middle" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M12 9V7H8V5h4V3l4 3-4 3zm-2 3H6V3L2 1h8v3h1V1c0-.55-.45-1-1-1H1C.45 0 0 .45 0 1v11.38c0 .39.22.73.55.91L6 16.01V13h4c.55 0 1-.45 1-1V8h-1v4z"/></svg>
        Sign out
      </button>
</form></nav>

    </div>

    <div class="Header-item Header-item--full flex-justify-center d-lg-none position-relative">
      <div class="css-truncate css-truncate-target width-fit position-absolute left-0 right-0 text-center">
              <svg class="octicon octicon-lock" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 13H3v-1h1v1zm8-6v7c0 .55-.45 1-1 1H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h1V4c0-2.2 1.8-4 4-4s4 1.8 4 4v2h1c.55 0 1 .45 1 1zM3.8 6h4.41V4c0-1.22-.98-2.2-2.2-2.2-1.22 0-2.2.98-2.2 2.2v2H3.8zM11 7H2v7h9V7zM4 8H3v1h1V8zm0 2H3v1h1v-1z"/></svg>
    <a class="Header-link" href="/mapbox">mapbox</a>
    /
    <a class="Header-link" href="/mapbox/help">help</a>

</div>
    </div>



    <div class="Header-item mr-0 mr-lg-3 flex-order-1 flex-lg-order-none">
      

    <a aria-label="You have unread notifications" class="Header-link notification-indicator position-relative tooltipped tooltipped-s js-socket-channel js-notification-indicator" data-hotkey="g n" data-ga-click="Header, go to notifications, icon:unread" data-channel="notification-changed:18397640" href="/notifications">
        <span class="mail-status unread"></span>
        <svg class="octicon octicon-bell" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M14 12v1H0v-1l.73-.58c.77-.77.81-2.55 1.19-4.42C2.69 3.23 6 2 6 2c0-.55.45-1 1-1s1 .45 1 1c0 0 3.39 1.23 4.16 5 .38 1.88.42 3.66 1.19 4.42l.66.58H14zm-7 4c1.11 0 2-.89 2-2H5c0 1.11.89 2 2 2z"/></svg>
</a>
    </div>


    <div class="Header-item position-relative d-none d-lg-flex">
      <details class="details-overlay details-reset">
  <summary class="Header-link"
      aria-label="Create new…"
      data-ga-click="Header, create new, icon:add">
    <svg class="octicon octicon-plus" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M12 9H7v5H5V9H0V7h5V2h2v5h5v2z"/></svg> <span class="dropdown-caret"></span>
  </summary>
  <details-menu class="dropdown-menu dropdown-menu-sw">
    
<a role="menuitem" class="dropdown-item" href="/new" data-ga-click="Header, create new repository">
  New repository
</a>

  <a role="menuitem" class="dropdown-item" href="/new/import" data-ga-click="Header, import a repository">
    Import repository
  </a>

<a role="menuitem" class="dropdown-item" href="https://gist.github.com/" data-ga-click="Header, create new gist">
  New gist
</a>

  <a role="menuitem" class="dropdown-item" href="/organizations/new" data-ga-click="Header, create new organization">
    New organization
  </a>


  <div role="none" class="dropdown-divider"></div>
  <div class="dropdown-header">
    <span title="mapbox/help">This repository</span>
  </div>
    <a role="menuitem" class="dropdown-item" href="/mapbox/help/issues/new" data-ga-click="Header, create new issue" data-skip-pjax>
      New issue
    </a>


  </details-menu>
</details>

    </div>

    <div class="Header-item position-relative mr-0 d-none d-lg-flex">
      
<details class="details-overlay details-reset">
  <summary class="Header-link"
    aria-label="View profile and more"
    data-ga-click="Header, show menu, icon:avatar">
    <img alt="@Jing-flyloveyin" class="avatar" src="https://avatars2.githubusercontent.com/u/18397640?s=40&amp;v=4" height="20" width="20">
    <span class="dropdown-caret"></span>
  </summary>
  <details-menu class="dropdown-menu dropdown-menu-sw mt-2" style="width: 180px">
    <div class="header-nav-current-user css-truncate"><a role="menuitem" class="no-underline user-profile-link px-3 pt-2 pb-2 mb-n2 mt-n1 d-block" href="/Jing-flyloveyin" data-ga-click="Header, go to profile, text:Signed in as">Signed in as <strong class="css-truncate-target">Jing-flyloveyin</strong></a></div>
    <div role="none" class="dropdown-divider"></div>

      <div class="pl-3 pr-3 f6 user-status-container js-user-status-context pb-1" data-url="/users/status?compact=1&amp;link_mentions=0&amp;truncate=1">
        
<div class="js-user-status-container
    user-status-compact rounded-1 px-2 py-1 mt-2
    border
  " data-team-hovercards-enabled>
  <details class="js-user-status-details details-reset details-overlay details-overlay-dark">
    <summary class="btn-link btn-block link-gray no-underline js-toggle-user-status-edit toggle-user-status-edit "
      role="menuitem" data-hydro-click="{&quot;event_type&quot;:&quot;user_profile.click&quot;,&quot;payload&quot;:{&quot;profile_user_id&quot;:600935,&quot;target&quot;:&quot;EDIT_USER_STATUS&quot;,&quot;user_id&quot;:18397640,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;CDFB:9475:9E852:EFEEE:5D701D80&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/building-a-store-locator.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;}}" data-hydro-click-hmac="a5be841bff640d5f0ccfa85469dc611c519c453a77b91ba64f327964e7114777">
      <div class="d-flex">
        <div class="f6 lh-condensed user-status-header
          d-inline-block v-align-middle
            user-status-emoji-only-header circle
            pr-2
"
            style="max-width: 29px"
          >
          <div class="user-status-emoji-container flex-shrink-0 mr-1  lh-condensed-ultra v-align-bottom" style="margin-top: 2px;">
            <div><g-emoji class="g-emoji" alias="dart" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f3af.png">🎯</g-emoji></div>
          </div>
        </div>
        <div class="
          d-inline-block v-align-middle
          
          
           css-truncate css-truncate-target 
           user-status-message-wrapper f6"
           style="line-height: 20px;" >
          <div class="d-inline-block text-gray-dark v-align-text-top text-left">
                <span>Focusing</span>
          </div>
        </div>
      </div>
    </summary>
    <details-dialog class="details-dialog rounded-1 anim-fade-in fast Box Box--overlay" role="dialog" tabindex="-1">
      <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="position-relative flex-auto js-user-status-form" action="/users/status?compact=1&amp;link_mentions=0&amp;truncate=1" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="_method" value="put" /><input type="hidden" name="authenticity_token" value="Z+BNw+8TUg4eFA/B+Cvm0mDpc+pypV8TqQZ7MZeucCYwHdEtJrfdMdvQ+se71Y97H5E8n7XeITuAihDlL1zrNw==" />
        <div class="Box-header bg-gray border-bottom p-3">
          <button class="Box-btn-octicon js-toggle-user-status-edit btn-octicon float-right" type="reset" aria-label="Close dialog" data-close-dialog>
            <svg class="octicon octicon-x" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48L7.48 8z"/></svg>
          </button>
          <h3 class="Box-title f5 text-bold text-gray-dark">Edit status</h3>
        </div>
        <input type="hidden" name="emoji" class="js-user-status-emoji-field" value=":dart:">
        <input type="hidden" name="organization_id" class="js-user-status-org-id-field" value="">
        <div class="px-3 py-2 text-gray-dark">
          <div class="js-characters-remaining-container position-relative mt-2">
            <div class="input-group d-table form-group my-0 js-user-status-form-group">
              <span class="input-group-button d-table-cell v-align-middle" style="width: 1%">
                <button type="button" aria-label="Choose an emoji" class="btn-outline btn js-toggle-user-status-emoji-picker btn-open-emoji-picker p-0">
                  <span class="js-user-status-original-emoji" hidden><div><g-emoji class="g-emoji" alias="dart" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f3af.png">🎯</g-emoji></div></span>
                  <span class="js-user-status-custom-emoji"><div><g-emoji class="g-emoji" alias="dart" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f3af.png">🎯</g-emoji></div></span>
                  <span class="js-user-status-no-emoji-icon" hidden>
                    <svg class="octicon octicon-smiley" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8s3.58 8 8 8 8-3.58 8-8-3.58-8-8-8zm4.81 12.81a6.72 6.72 0 0 1-2.17 1.45c-.83.36-1.72.53-2.64.53-.92 0-1.81-.17-2.64-.53-.81-.34-1.55-.83-2.17-1.45a6.773 6.773 0 0 1-1.45-2.17A6.59 6.59 0 0 1 1.21 8c0-.92.17-1.81.53-2.64.34-.81.83-1.55 1.45-2.17.62-.62 1.36-1.11 2.17-1.45A6.59 6.59 0 0 1 8 1.21c.92 0 1.81.17 2.64.53.81.34 1.55.83 2.17 1.45.62.62 1.11 1.36 1.45 2.17.36.83.53 1.72.53 2.64 0 .92-.17 1.81-.53 2.64-.34.81-.83 1.55-1.45 2.17zM4 6.8v-.59c0-.66.53-1.19 1.2-1.19h.59c.66 0 1.19.53 1.19 1.19v.59c0 .67-.53 1.2-1.19 1.2H5.2C4.53 8 4 7.47 4 6.8zm5 0v-.59c0-.66.53-1.19 1.2-1.19h.59c.66 0 1.19.53 1.19 1.19v.59c0 .67-.53 1.2-1.19 1.2h-.59C9.53 8 9 7.47 9 6.8zm4 3.2c-.72 1.88-2.91 3-5 3s-4.28-1.13-5-3c-.14-.39.23-1 .66-1h8.59c.41 0 .89.61.75 1z"/></svg>
                  </span>
                </button>
              </span>
              <text-expander keys=": @" data-mention-url="/autocomplete/user-suggestions" data-emoji-url="/autocomplete/emoji">
                <input
                  type="text"
                  autocomplete="off"
                  data-no-org-url="/autocomplete/user-suggestions"
                  data-org-url="/suggestions?mention_suggester=1"
                  data-maxlength="80"
                  class="d-table-cell width-full form-control js-user-status-message-field js-characters-remaining-field"
                  placeholder="What's happening?"
                  name="message"
                  value="Focusing"
                  aria-label="What is your current status?">
              </text-expander>
              <div class="error">Could not update your status, please try again.</div>
            </div>
            <div style="margin-left: 53px" class="my-1 text-small label-characters-remaining js-characters-remaining" data-suffix="remaining" hidden>
              80 remaining
            </div>
          </div>
          <include-fragment class="js-user-status-emoji-picker" data-url="/users/status/emoji"></include-fragment>
          <div class="overflow-auto ml-n3 mr-n3 px-3 border-bottom" style="max-height: 33vh">
            <div class="user-status-suggestions js-user-status-suggestions collapsed overflow-hidden">
              <h4 class="f6 text-normal my-3">Suggestions:</h4>
              <div class="mx-3 mt-2 clearfix">
                  <div class="float-left col-6">
                      <button type="button" value=":palm_tree:" class="d-flex flex-items-baseline flex-items-stretch lh-condensed f6 btn-link link-gray no-underline js-predefined-user-status mb-1">
                        <div class="emoji-status-width mr-2 v-align-middle js-predefined-user-status-emoji">
                          <g-emoji alias="palm_tree" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f334.png">🌴</g-emoji>
                        </div>
                        <div class="d-flex flex-items-center no-underline js-predefined-user-status-message ws-normal text-left" style="border-left: 1px solid transparent">
                          On vacation
                        </div>
                      </button>
                      <button type="button" value=":face_with_thermometer:" class="d-flex flex-items-baseline flex-items-stretch lh-condensed f6 btn-link link-gray no-underline js-predefined-user-status mb-1">
                        <div class="emoji-status-width mr-2 v-align-middle js-predefined-user-status-emoji">
                          <g-emoji alias="face_with_thermometer" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f912.png">🤒</g-emoji>
                        </div>
                        <div class="d-flex flex-items-center no-underline js-predefined-user-status-message ws-normal text-left" style="border-left: 1px solid transparent">
                          Out sick
                        </div>
                      </button>
                  </div>
                  <div class="float-left col-6">
                      <button type="button" value=":house:" class="d-flex flex-items-baseline flex-items-stretch lh-condensed f6 btn-link link-gray no-underline js-predefined-user-status mb-1">
                        <div class="emoji-status-width mr-2 v-align-middle js-predefined-user-status-emoji">
                          <g-emoji alias="house" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f3e0.png">🏠</g-emoji>
                        </div>
                        <div class="d-flex flex-items-center no-underline js-predefined-user-status-message ws-normal text-left" style="border-left: 1px solid transparent">
                          Working from home
                        </div>
                      </button>
                      <button type="button" value=":dart:" class="d-flex flex-items-baseline flex-items-stretch lh-condensed f6 btn-link link-gray no-underline js-predefined-user-status mb-1">
                        <div class="emoji-status-width mr-2 v-align-middle js-predefined-user-status-emoji">
                          <g-emoji alias="dart" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/1f3af.png">🎯</g-emoji>
                        </div>
                        <div class="d-flex flex-items-center no-underline js-predefined-user-status-message ws-normal text-left" style="border-left: 1px solid transparent">
                          Focusing
                        </div>
                      </button>
                  </div>
              </div>
            </div>
            <div class="user-status-limited-availability-container">
              <div class="form-checkbox my-0">
                <input type="checkbox" name="limited_availability" value="1" class="js-user-status-limited-availability-checkbox" data-default-message="I may be slow to respond." aria-describedby="limited-availability-help-text-truncate-true-compact-true" id="limited-availability-truncate-true-compact-true">
                <label class="d-block f5 text-gray-dark mb-1" for="limited-availability-truncate-true-compact-true">
                  Busy
                </label>
                <p class="note" id="limited-availability-help-text-truncate-true-compact-true">
                  When others mention you, assign you, or request your review,
                  GitHub will let them know that you have limited availability.
                </p>
              </div>
            </div>
          </div>
            

<div class="d-inline-block f5 mr-2 pt-3 pb-2" >
  <div class="d-inline-block mr-1">
    Clear status
  </div>

  <details class="js-user-status-expire-drop-down f6 dropdown details-reset details-overlay d-inline-block mr-2">
    <summary class="f5 btn-link link-gray-dark border px-2 py-1 rounded-1" aria-haspopup="true">
      <div class="js-user-status-expiration-interval-selected d-inline-block v-align-baseline">
        Never
      </div>
      <div class="dropdown-caret"></div>
    </summary>

    <ul class="dropdown-menu dropdown-menu-se pl-0 overflow-auto" style="width: 220px; max-height: 15.5em">
      <li>
        <button type="button" class="btn-link dropdown-item js-user-status-expire-button ws-normal" title="Never">
          <span class="d-inline-block text-bold mb-1">Never</span>
          <div class="f6 lh-condensed">Keep this status until you clear your status or edit your status.</div>
        </button>
      </li>
      <li class="dropdown-divider" role="none"></li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 30 minutes" value="2019-09-04T13:54:38-07:00">
            in 30 minutes
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 1 hour" value="2019-09-04T14:24:38-07:00">
            in 1 hour
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 4 hours" value="2019-09-04T17:24:38-07:00">
            in 4 hours
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="today" value="2019-09-04T23:59:59-07:00">
            today
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="this week" value="2019-09-08T23:59:59-07:00">
            this week
          </button>
        </li>
    </ul>
  </details>
  <input class="js-user-status-expiration-date-input" type="hidden" name="expires_at" value="">
</div>

          <include-fragment class="js-user-status-org-picker" data-url="/users/status/organizations"></include-fragment>
        </div>
        <div class="d-flex flex-items-center flex-justify-between p-3 border-top">
          <button type="submit"  class="width-full btn btn-primary mr-2 js-user-status-submit">
            Set status
          </button>
          <button type="button"  class="width-full js-clear-user-status-button btn ml-2 js-user-status-exists">
            Clear status
          </button>
        </div>
</form>    </details-dialog>
  </details>
</div>

      </div>
      <div role="none" class="dropdown-divider"></div>


    <a role="menuitem" class="dropdown-item" href="/Jing-flyloveyin" data-ga-click="Header, go to profile, text:your profile">Your profile</a>


    <a role="menuitem" class="dropdown-item" href="/Jing-flyloveyin?tab=repositories" data-ga-click="Header, go to repositories, text:your repositories">Your repositories</a>

    <a role="menuitem" class="dropdown-item" href="/Jing-flyloveyin?tab=projects" data-ga-click="Header, go to projects, text:your projects">Your projects</a>

    <a role="menuitem" class="dropdown-item" href="/Jing-flyloveyin?tab=stars" data-ga-click="Header, go to starred repos, text:your stars">Your stars</a>
      <a role="menuitem" class="dropdown-item" href="https://gist.github.com/mine" data-ga-click="Header, your gists, text:your gists">Your gists</a>


    <div role="none" class="dropdown-divider"></div>
    <a role="menuitem" class="dropdown-item" href="https://help.github.com" data-ga-click="Header, go to help, text:help">Help</a>
    <a role="menuitem" class="dropdown-item" href="/settings/profile" data-ga-click="Header, go to settings, icon:settings">Settings</a>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="logout-form" action="/logout" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="Seba4tR66muNiw2RwJZVhEOysj8VnhvRPxaqT0+ispINNOPZxo683C9Q5vWq5rkKLMney7ZwDhLBNcdMVfi+Mg==" />
      
      <button type="submit" class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout" role="menuitem">
        Sign out
      </button>
</form>  </details-menu>
</details>

    </div>

  </header>

      

  </div>

  <div id="start-of-content" class="show-on-focus"></div>


    <div id="js-flash-container">

</div>



  <div class="application-main " data-commit-hovercards-enabled>
        <div itemscope itemtype="http://schema.org/SoftwareSourceCode" class="">
    <main  >
      


  

      <div class="border-bottom shelf intro-shelf js-notice mb-0 pb-4">
  <div class="width-full container">
    <div class="width-full mx-auto shelf-content">
      <h2 class="shelf-title">Learn Git and GitHub without any code!</h2>
      <p class="shelf-lead">
          Using the Hello World guide, you’ll start a branch, write comments, and open a pull request.
      </p>
      <a class="btn btn-primary shelf-cta" target="_blank" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;READ_GUIDE&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;CDFB:9475:9E852:EFEEE:5D701D80&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/building-a-store-locator.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="10cc62157f66535fe8a5a36a87fa0909b9117c56e25eca90718579f47c59e96b" href="https://guides.github.com/activities/hello-world/">Read the guide</a>
    </div>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="shelf-dismiss js-notice-dismiss" action="/dashboard/dismiss_bootcamp" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="_method" value="delete" /><input type="hidden" name="authenticity_token" value="kXP+LMC2rg0T1sBhKqQUoraLvUJdA+rJw7pV7tQ5Tdat0Rg1SCOp88/Q8C51SrKcHqtO/qPDyg3TGrMT/KURYg==" />
      <button name="button" type="submit" class="mr-1 close-button tooltipped tooltipped-w" aria-label="Hide this notice forever" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;DISMISS_BANNER&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;CDFB:9475:9E852:EFEEE:5D701D80&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/building-a-store-locator.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="59934c2af69315c18b3b9fca2627dd1b2e559d4df76ce2601d67e51d382e3316">
        <svg aria-label="Hide this notice forever" class="octicon octicon-x v-align-text-top" viewBox="0 0 12 16" version="1.1" width="12" height="16" role="img"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48L7.48 8z"/></svg>
</button></form>  </div>
</div>



  








  <div class="pagehead repohead instapaper_ignore readability-menu experiment-repo-nav pt-0 pt-lg-4 ">
    <div class="repohead-details-container clearfix container-lg p-responsive d-none d-lg-block">

      <ul class="pagehead-actions">




  <li>
    
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form data-remote="true" class="clearfix js-social-form js-social-container" action="/notifications/subscribe" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="J1ZfcgIjFyD9HauqqbtO1YM/dMpJfezxuEmPGYv0A3WLLYBgXeOAwsBVB2K3rL5M17DhqYf1hidGoAyb33XkBQ==" />      <input type="hidden" name="repository_id" value="34758294">

      <details class="details-reset details-overlay select-menu float-left">
        <summary class="select-menu-button float-left btn btn-sm btn-with-count" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;WATCH_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;CDFB:9475:9E852:EFEEE:5D701D80&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/building-a-store-locator.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="430cf82dee12fa6693ec4e8eaa2c98ee56963b825aad89004a61cbe60e185b6f" data-ga-click="Repository, click Watch settings, action:blob#show">          <span data-menu-button>
              <svg class="octicon octicon-eye v-align-text-bottom" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
              Watch
          </span>
</summary>        <details-menu
          class="select-menu-modal position-absolute mt-5"
          style="z-index: 99;">
          <div class="select-menu-header">
            <span class="select-menu-title">Notifications</span>
          </div>
          <div class="select-menu-list">
            <button type="submit" name="do" value="included" class="select-menu-item width-full" aria-checked="true" role="menuitemradio">
              <svg class="octicon octicon-check select-menu-item-icon" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5L12 5z"/></svg>
              <div class="select-menu-item-text">
                <span class="select-menu-item-heading">Not watching</span>
                <span class="description">Be notified only when participating or @mentioned.</span>
                <span class="hidden-select-button-text" data-menu-button-contents>
                  <svg class="octicon octicon-eye v-align-text-bottom" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                  Watch
                </span>
              </div>
            </button>

            <button type="submit" name="do" value="release_only" class="select-menu-item width-full" aria-checked="false" role="menuitemradio">
              <svg class="octicon octicon-check select-menu-item-icon" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5L12 5z"/></svg>
              <div class="select-menu-item-text">
                <span class="select-menu-item-heading">Releases only</span>
                <span class="description">Be notified of new releases, and when participating or @mentioned.</span>
                <span class="hidden-select-button-text" data-menu-button-contents>
                  <svg class="octicon octicon-eye v-align-text-bottom" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                  Unwatch releases
                </span>
              </div>
            </button>

            <button type="submit" name="do" value="subscribed" class="select-menu-item width-full" aria-checked="false" role="menuitemradio">
              <svg class="octicon octicon-check select-menu-item-icon" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5L12 5z"/></svg>
              <div class="select-menu-item-text">
                <span class="select-menu-item-heading">Watching</span>
                <span class="description">Be notified of all conversations.</span>
                <span class="hidden-select-button-text" data-menu-button-contents>
                  <svg class="octicon octicon-eye v-align-text-bottom" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                  Unwatch
                </span>
              </div>
            </button>

            <button type="submit" name="do" value="ignore" class="select-menu-item width-full" aria-checked="false" role="menuitemradio">
              <svg class="octicon octicon-check select-menu-item-icon" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5L12 5z"/></svg>
              <div class="select-menu-item-text">
                <span class="select-menu-item-heading">Ignoring</span>
                <span class="description">Never be notified.</span>
                <span class="hidden-select-button-text" data-menu-button-contents>
                  <svg class="octicon octicon-mute v-align-text-bottom" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8 2.81v10.38c0 .67-.81 1-1.28.53L3 10H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h2l3.72-3.72C7.19 1.81 8 2.14 8 2.81zm7.53 3.22l-1.06-1.06-1.97 1.97-1.97-1.97-1.06 1.06L11.44 8 9.47 9.97l1.06 1.06 1.97-1.97 1.97 1.97 1.06-1.06L13.56 8l1.97-1.97z"/></svg>
                  Stop ignoring
                </span>
              </div>
            </button>
          </div>
        </details-menu>
      </details>
        <a class="social-count js-social-count"
          href="/mapbox/help/watchers"
          aria-label="45 users are watching this repository">
          45
        </a>
</form>
  </li>

  <li>
      <div class="js-toggler-container js-social-container starring-container ">
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="starred js-social-form" action="/mapbox/help/unstar" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="dFZeiEnAewsa6rn44Y5JHIHREa69MW/fO2sCetftsbQT0LihgXiQWkpRV4PNF6++zZVMCIrSqb8KJrFnMCH+rw==" />
      <input type="hidden" name="context" value="repository"></input>
      <button type="submit" class="btn btn-sm btn-with-count js-toggler-target" aria-label="Unstar this repository" title="Unstar mapbox/help" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;UNSTAR_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;CDFB:9475:9E852:EFEEE:5D701D80&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/building-a-store-locator.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="ff6bbd861ad8b9b484a91906733b12d71833bebe5d2adaa7ecb6471c3e3db6ab" data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">        <svg class="octicon octicon-star v-align-text-bottom" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74L14 6z"/></svg>
        Unstar
</button>        <a class="social-count js-social-count" href="/mapbox/help/stargazers"
           aria-label="3 users starred this repository">
           3
        </a>
</form>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="unstarred js-social-form" action="/mapbox/help/star" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="48/24EaBvJjMyp2djM6x7A0rWyvoK6IWLhqpub3KGiWCZkFZk5XLW0SpQxG4coE6e7fm87bMfrPNihHmvtZGzg==" />
      <input type="hidden" name="context" value="repository"></input>
      <button type="submit" class="btn btn-sm btn-with-count js-toggler-target" aria-label="Unstar this repository" title="Star mapbox/help" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;STAR_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;CDFB:9475:9E852:EFEEE:5D701D80&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/building-a-store-locator.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="71ac3d218403daabed0934f6134dcb0647a19438f3df45a942d5ceebd116b7b5" data-ga-click="Repository, click star button, action:blob#show; text:Star">        <svg class="octicon octicon-star v-align-text-bottom" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74L14 6z"/></svg>
        Star
</button>        <a class="social-count js-social-count" href="/mapbox/help/stargazers"
           aria-label="3 users starred this repository">
          3
        </a>
</form>  </div>

  </li>

  <li>
        <span class="btn btn-sm btn-with-count disabled tooltipped tooltipped-sw" aria-label="Cannot fork because forking is disabled.">
          <svg class="octicon octicon-repo-forked v-align-text-bottom" viewBox="0 0 10 16" version="1.1" width="10" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8 1a1.993 1.993 0 0 0-1 3.72V6L5 8 3 6V4.72A1.993 1.993 0 0 0 2 1a1.993 1.993 0 0 0-1 3.72V6.5l3 3v1.78A1.993 1.993 0 0 0 5 15a1.993 1.993 0 0 0 1-3.72V9.5l3-3V4.72A1.993 1.993 0 0 0 8 1zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3 10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3-10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
          Fork
</span>
    <a href="/mapbox/help/network/members" class="social-count"
       aria-label="0 users forked this repository">
      0
    </a>
  </li>
</ul>

      <h1 class="private ">
    <svg class="octicon octicon-lock" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 13H3v-1h1v1zm8-6v7c0 .55-.45 1-1 1H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h1V4c0-2.2 1.8-4 4-4s4 1.8 4 4v2h1c.55 0 1 .45 1 1zM3.8 6h4.41V4c0-1.22-.98-2.2-2.2-2.2-1.22 0-2.2.98-2.2 2.2v2H3.8zM11 7H2v7h9V7zM4 8H3v1h1V8zm0 2H3v1h1v-1z"/></svg>
  <span class="author" itemprop="author"><a class="url fn" rel="author" data-hovercard-type="organization" data-hovercard-url="/orgs/mapbox/hovercard" href="/mapbox">mapbox</a></span><!--
--><span class="path-divider">/</span><!--
--><strong itemprop="name"><a data-pjax="#js-repo-pjax-container" href="/mapbox/help">help</a></strong>
  <span class="Label Label--outline v-align-middle ">Private</span>

</h1>

    </div>
    
<nav class="hx_reponav reponav js-repo-nav js-sidenav-container-pjax container-lg p-responsive d-none d-lg-block"
     itemscope
     itemtype="http://schema.org/BreadcrumbList"
    aria-label="Repository"
     data-pjax="#js-repo-pjax-container">

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a class="js-selected-navigation-item selected reponav-item" itemprop="url" data-hotkey="g c" aria-current="page" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches repo_packages /mapbox/help" href="/mapbox/help">
      <svg class="octicon octicon-code" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M9.5 3L8 4.5 11.5 8 8 11.5 9.5 13 14 8 9.5 3zm-5 0L0 8l4.5 5L6 11.5 2.5 8 6 4.5 4.5 3z"/></svg>
      <span itemprop="name">Code</span>
      <meta itemprop="position" content="1">
</a>  </span>

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a itemprop="url" data-hotkey="g i" class="js-selected-navigation-item reponav-item" data-selected-links="repo_issues repo_labels repo_milestones /mapbox/help/issues" href="/mapbox/help/issues">
        <svg class="octicon octicon-issue-opened" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7 2.3c3.14 0 5.7 2.56 5.7 5.7s-2.56 5.7-5.7 5.7A5.71 5.71 0 0 1 1.3 8c0-3.14 2.56-5.7 5.7-5.7zM7 1C3.14 1 0 4.14 0 8s3.14 7 7 7 7-3.14 7-7-3.14-7-7-7zm1 3H6v5h2V4zm0 6H6v2h2v-2z"/></svg>
        <span itemprop="name">Issues</span>
        <span class="Counter">71</span>
        <meta itemprop="position" content="2">
</a>    </span>

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a data-hotkey="g p" itemprop="url" class="js-selected-navigation-item reponav-item" data-selected-links="repo_pulls checks /mapbox/help/pulls" href="/mapbox/help/pulls">
      <svg class="octicon octicon-git-pull-request" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M11 11.28V5c-.03-.78-.34-1.47-.94-2.06C9.46 2.35 8.78 2.03 8 2H7V0L4 3l3 3V4h1c.27.02.48.11.69.31.21.2.3.42.31.69v6.28A1.993 1.993 0 0 0 10 15a1.993 1.993 0 0 0 1-3.72zm-1 2.92c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zM4 3c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v6.56A1.993 1.993 0 0 0 2 15a1.993 1.993 0 0 0 1-3.72V4.72c.59-.34 1-.98 1-1.72zm-.8 10c0 .66-.55 1.2-1.2 1.2-.65 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
      <span itemprop="name">Pull requests</span>
      <span class="Counter">12</span>
      <meta itemprop="position" content="3">
</a>  </span>


    <a data-hotkey="g b" class="js-selected-navigation-item reponav-item" data-selected-links="repo_projects new_repo_project repo_project /mapbox/help/projects" href="/mapbox/help/projects">
      <svg class="octicon octicon-project" viewBox="0 0 15 16" version="1.1" width="15" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M10 12h3V2h-3v10zm-4-2h3V2H6v8zm-4 4h3V2H2v12zm-1 1h13V1H1v14zM14 0H1a1 1 0 0 0-1 1v14a1 1 0 0 0 1 1h13a1 1 0 0 0 1-1V1a1 1 0 0 0-1-1z"/></svg>
      Projects
      <span class="Counter" >1</span>
</a>

    <a class="js-selected-navigation-item reponav-item" data-hotkey="g w" data-selected-links="repo_wiki /mapbox/help/wiki" href="/mapbox/help/wiki">
      <svg class="octicon octicon-book" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M3 5h4v1H3V5zm0 3h4V7H3v1zm0 2h4V9H3v1zm11-5h-4v1h4V5zm0 2h-4v1h4V7zm0 2h-4v1h4V9zm2-6v9c0 .55-.45 1-1 1H9.5l-1 1-1-1H2c-.55 0-1-.45-1-1V3c0-.55.45-1 1-1h5.5l1 1 1-1H15c.55 0 1 .45 1 1zm-8 .5L7.5 3H2v9h6V3.5zm7-.5H9.5l-.5.5V12h6V3z"/></svg>
      Wiki
</a>
    <a data-skip-pjax="true" class="js-selected-navigation-item reponav-item" data-selected-links="security alerts policy code_scanning /mapbox/help/security/advisories" href="/mapbox/help/security/advisories">
      <svg class="octicon octicon-shield" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M0 2l7-2 7 2v6.02C14 12.69 8.69 16 7 16c-1.69 0-7-3.31-7-7.98V2zm1 .75L7 1l6 1.75v5.268C13 12.104 8.449 15 7 15c-1.449 0-6-2.896-6-6.982V2.75zm1 .75L7 2v12c-1.207 0-5-2.482-5-5.985V3.5z"/></svg>
      Security
</a>
    <a class="js-selected-navigation-item reponav-item" data-selected-links="repo_graphs repo_contributors dependency_graph pulse people /mapbox/help/pulse" href="/mapbox/help/pulse">
      <svg class="octicon octicon-graph" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M16 14v1H0V0h1v14h15zM5 13H3V8h2v5zm4 0H7V3h2v10zm4 0h-2V6h2v7z"/></svg>
      Insights
</a>

</nav>

  <div class="reponav-wrapper reponav-small d-lg-none">
  <nav class="reponav js-reponav text-center no-wrap"
       itemscope
       itemtype="http://schema.org/BreadcrumbList">

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a class="js-selected-navigation-item selected reponav-item" itemprop="url" aria-current="page" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches repo_packages /mapbox/help" href="/mapbox/help">
        <span itemprop="name">Code</span>
        <meta itemprop="position" content="1">
</a>    </span>

      <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
        <a itemprop="url" class="js-selected-navigation-item reponav-item" data-selected-links="repo_issues repo_labels repo_milestones /mapbox/help/issues" href="/mapbox/help/issues">
          <span itemprop="name">Issues</span>
          <span class="Counter">71</span>
          <meta itemprop="position" content="2">
</a>      </span>

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a itemprop="url" class="js-selected-navigation-item reponav-item" data-selected-links="repo_pulls checks /mapbox/help/pulls" href="/mapbox/help/pulls">
        <span itemprop="name">Pull requests</span>
        <span class="Counter">12</span>
        <meta itemprop="position" content="3">
</a>    </span>

      <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
        <a itemprop="url" class="js-selected-navigation-item reponav-item" data-selected-links="repo_projects new_repo_project repo_project /mapbox/help/projects" href="/mapbox/help/projects">
          <span itemprop="name">Projects</span>
          <span class="Counter">1</span>
          <meta itemprop="position" content="4">
</a>      </span>

      <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
        <a itemprop="url" class="js-selected-navigation-item reponav-item" data-selected-links="repo_wiki /mapbox/help/wiki" href="/mapbox/help/wiki">
          <span itemprop="name">Wiki</span>
          <meta itemprop="position" content="5">
</a>      </span>

      <a itemprop="url" class="js-selected-navigation-item reponav-item" data-selected-links="security alerts policy code_scanning /mapbox/help/security/advisories" href="/mapbox/help/security/advisories">
        <span itemprop="name">Security</span>
        <meta itemprop="position" content="6">
</a>
      <a class="js-selected-navigation-item reponav-item" data-selected-links="pulse /mapbox/help/pulse" href="/mapbox/help/pulse">
        Pulse
</a>

  </nav>
</div>


  </div>
<div class="container-lg clearfix new-discussion-timeline experiment-repo-nav  p-responsive">
  <div class="repository-content ">

    
    


  


    <a class="d-none js-permalink-shortcut" data-hotkey="y" href="/mapbox/help/blob/965b7620e7e1124ef6ac3d7b8dd90287324eae45/src/pages/tutorials/building-a-store-locator.md">Permalink</a>

    <!-- blob contrib key: blob_contributors:v21:e1ca442725f78451833bf0ca4c837632 -->
      

    <div class="d-flex flex-items-start flex-shrink-0 pb-3 flex-column flex-md-row">
      <span class="d-flex flex-justify-between width-full width-md-auto">
        
<details class="details-reset details-overlay select-menu branch-select-menu  hx_rsm" id="branch-select-menu">
  <summary class="btn btn-sm select-menu-button css-truncate"
           data-hotkey="w"
           title="publisher-production">
    <i>Branch:</i>
    <span class="css-truncate-target" data-menu-button>publisher-prod…</span>
  </summary>

  <details-menu class="select-menu-modal hx_rsm-modal position-absolute" style="z-index: 99;" src="/mapbox/help/ref-list/publisher-production/src/pages/tutorials/building-a-store-locator.md?source_action=show&amp;source_controller=blob" preload>
    <include-fragment class="select-menu-loading-overlay anim-pulse">
      <svg height="32" class="octicon octicon-octoface" viewBox="0 0 16 16" version="1.1" width="32" aria-hidden="true"><path fill-rule="evenodd" d="M14.7 5.34c.13-.32.55-1.59-.13-3.31 0 0-1.05-.33-3.44 1.3-1-.28-2.07-.32-3.13-.32s-2.13.04-3.13.32c-2.39-1.64-3.44-1.3-3.44-1.3-.68 1.72-.26 2.99-.13 3.31C.49 6.21 0 7.33 0 8.69 0 13.84 3.33 15 7.98 15S16 13.84 16 8.69c0-1.36-.49-2.48-1.3-3.35zM8 14.02c-3.3 0-5.98-.15-5.98-3.35 0-.76.38-1.48 1.02-2.07 1.07-.98 2.9-.46 4.96-.46 2.07 0 3.88-.52 4.96.46.65.59 1.02 1.3 1.02 2.07 0 3.19-2.68 3.35-5.98 3.35zM5.49 9.01c-.66 0-1.2.8-1.2 1.78s.54 1.79 1.2 1.79c.66 0 1.2-.8 1.2-1.79s-.54-1.78-1.2-1.78zm5.02 0c-.66 0-1.2.79-1.2 1.78s.54 1.79 1.2 1.79c.66 0 1.2-.8 1.2-1.79s-.53-1.78-1.2-1.78z"/></svg>
    </include-fragment>
  </details-menu>
</details>

        <div class="BtnGroup flex-shrink-0 d-md-none">
          <a href="/mapbox/help/find/publisher-production"
                class="js-pjax-capture-input btn btn-sm BtnGroup-item"
                data-pjax
                data-hotkey="t">
            Find file
          </a>
          <clipboard-copy value="src/pages/tutorials/building-a-store-locator.md" class="btn btn-sm BtnGroup-item">
            Copy path
          </clipboard-copy>
        </div>
      </span>
      <h2 id="blob-path" class="breadcrumb flex-auto min-width-0 text-normal flex-md-self-center ml-md-2 mr-md-3 my-2 my-md-0">
        <span class="js-repo-root text-bold"><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help"><span>help</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src"><span>src</span></a></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src/pages"><span>pages</span></a></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src/pages/tutorials"><span>tutorials</span></a></span><span class="separator">/</span><strong class="final-path">building-a-store-locator.md</strong>
      </h2>

      <div class="BtnGroup flex-shrink-0 d-none d-md-inline-block">
        <a href="/mapbox/help/find/publisher-production"
              class="js-pjax-capture-input btn btn-sm BtnGroup-item"
              data-pjax
              data-hotkey="t">
          Find file
        </a>
        <clipboard-copy value="src/pages/tutorials/building-a-store-locator.md" class="btn btn-sm BtnGroup-item">
          Copy path
        </clipboard-copy>
      </div>
    </div>



    <include-fragment src="/mapbox/help/contributors/publisher-production/src/pages/tutorials/building-a-store-locator.md" class="Box Box--condensed commit-loader">
      <div class="Box-body bg-blue-light f6">
        Fetching contributors&hellip;
      </div>

      <div class="Box-body d-flex flex-items-center" >
          <img alt="" class="loader-loading mr-2" src="https://github.githubassets.com/images/spinners/octocat-spinner-32-EAF2F5.gif" width="16" height="16" />
        <span class="text-red h6 loader-error">Cannot retrieve contributors at this time</span>
      </div>
</include-fragment>




    <div class="Box mt-3 position-relative">
      
<div class="Box-header py-2 d-flex flex-column flex-shrink-0 flex-md-row flex-md-items-center">

  <div class="text-mono f6 flex-auto pr-3 flex-order-2 flex-md-order-1 mt-2 mt-md-0">
      616 lines (489 sloc)
      <span class="file-info-divider"></span>
    19.4 KB
  </div>

  <div class="d-flex py-1 py-md-0 flex-auto flex-order-1 flex-md-order-2 flex-sm-grow-0 flex-justify-between">

    <div class="BtnGroup">
      <a id="raw-url" class="btn btn-sm BtnGroup-item" href="/mapbox/help/raw/publisher-production/src/pages/tutorials/building-a-store-locator.md">Raw</a>
        <a class="btn btn-sm js-update-url-with-hash BtnGroup-item" data-hotkey="b" href="/mapbox/help/blame/publisher-production/src/pages/tutorials/building-a-store-locator.md">Blame</a>
      <a rel="nofollow" class="btn btn-sm BtnGroup-item" href="/mapbox/help/commits/publisher-production/src/pages/tutorials/building-a-store-locator.md">History</a>
    </div>


    <div>
            <a class="btn-octicon tooltipped tooltipped-nw"
               href="x-github-client://openRepo/https://github.com/mapbox/help?branch=publisher-production&amp;filepath=src%2Fpages%2Ftutorials%2Fbuilding-a-store-locator.md"
               aria-label="Open this file in GitHub Desktop"
               data-ga-click="Repository, open with desktop, type:mac">
                <svg class="octicon octicon-device-desktop" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"/></svg>
            </a>

            <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="inline-form js-update-url-with-hash" action="/mapbox/help/edit/publisher-production/src/pages/tutorials/building-a-store-locator.md" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="BtqvL52OPk2FsxjLh/GUKnwCK0DwgTOBJV/mrmEuFmU7PQ+fkzhSdlQelxs1ubBDb1V17mIb41cIeP9CCHUVeg==" />
              <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
                aria-label="Edit this file" data-hotkey="e" data-disable-with>
                <svg class="octicon octicon-pencil" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"/></svg>
              </button>
</form>
          <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="inline-form" action="/mapbox/help/delete/publisher-production/src/pages/tutorials/building-a-store-locator.md" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="mKfR/gsSbY2Acgk9Hnwhy1CvNbP1/gDdymP/6nQ8whm3WjMcB0IhNnoHT8vFDgS4GCO6giVWilPmedC7KcqaJQ==" />
            <button class="btn-octicon btn-octicon-danger tooltipped tooltipped-nw" type="submit"
              aria-label="Delete this file" data-disable-with>
              <svg class="octicon octicon-trashcan" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M11 2H9c0-.55-.45-1-1-1H5c-.55 0-1 .45-1 1H2c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1v9c0 .55.45 1 1 1h7c.55 0 1-.45 1-1V5c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm-1 12H3V5h1v8h1V5h1v8h1V5h1v8h1V5h1v9zm1-10H2V3h9v1z"/></svg>
            </button>
</form>    </div>
  </div>
</div>




      
  <div id="readme" class="Box-body readme blob instapaper_body js-code-block-container">
    <article class="markdown-body entry-content p-3 p-md-6" itemprop="text"><table data-table-type="yaml-metadata">
  <thead>
  <tr>
  <th>title</th>
  <th>description</th>
  <th>thumbnail</th>
  <th>level</th>
  <th>topics</th>
  <th>language</th>
  <th>prereq</th>
  <th>prependJs</th>
  <th>contentType</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div>Build a store locator using Mapbox GL JS</div></td>
  <td><div>Build a map application with Mapbox GL JS. This guide walks you through all the code that you need to build a store locator.</div></td>
  <td><div>buildingAStoreLocator</div></td>
  <td><div>3</div></td>
  <td><div><table>
  <tbody>
  <tr>
  <td><div>web apps</div></td>
  </tr>
  </tbody>
</table>
</div></td>
  <td><div><table>
  <tbody>
  <tr>
  <td><div>JavaScript</div></td>
  </tr>
  </tbody>
</table>
</div></td>
  <td><div>Familiarity with front-end development concepts. Some advanced JavaScript required.</div></td>
  <td><div><table>
  <tbody>
  <tr>
  <td><div>import * as constants from '../../constants';</div></td>
  <td><div>import Icon from '@mapbox/mr-ui/icon';</div></td>
  <td><div>import { sweetgreenLocations } from '../../snippets/sweetgreen-locations';</div></td>
  <td><div>import UserAccessToken from '../../components/user-access-token';</div></td>
  <td><div>import DemoIframe from '@mapbox/dr-ui/demo-iframe';</div></td>
  <td><div>import { DemoLink } from '../../components/demo-link';</div></td>
  <td><div>import Button from '@mapbox/mr-ui/button';</div></td>
  </tr>
  </tbody>
</table>
</div></td>
  <td><div>tutorial</div></td>
  </tr>
  </tbody>
</table>

<p>This guide will walk you through how to create a store locator map using Mapbox GL JS. You'll be able to browse all the locations from a sidebar and select a specific store to view more information. Selecting a <a href="/mapbox/help/blob/publisher-production/help/glossary/marker">marker</a> on the map will highlight the selected store on the sidebar.</p>
<p>{{

}}</p>
<p>You will use <a href="http://sweetgreen.com" rel="nofollow">Sweetgreen</a>, a local salad shop, as an example. They have a healthy number of locations, plus their salads are delicious!</p>
<p>This guide shows you how to use <a href="https://www.mapbox.com/mapbox-gl-js/" rel="nofollow">Mapbox GL JS</a> to build an interactive web map. If you're new to Mapbox GL JS, you might want to read our guide on Mapbox <a href="/mapbox/help/blob/publisher-production/help/how-mapbox-works/web-apps">web applications</a> first.</p>
<h2><a id="user-content-getting-started" class="anchor" aria-hidden="true" href="#getting-started"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Getting started</h2>
<p>For this project, we recommend that you create a local folder called "store-locator" to house your project files. You'll see this folder referred to as your <em>project folder</em>.</p>
<p>There are a few resources you'll need before getting started:</p>
<ul>
<li>
<p><a href="/mapbox/help/blob/publisher-production/help/glossary/style-url"><strong>A style URL</strong></a>. A style URL points to a unique map you have created with Mapbox Studio. You can either create a custom style with the <a href="https://www.mapbox.com/studio-manual/reference/styles/" rel="nofollow">Mapbox Studio style editor</a> or use a <a href="https://www.mapbox.com/studio/styles" rel="nofollow">Mapbox style</a>.</p>
</li>
<li>
<p><a href="/mapbox/help/blob/publisher-production/help/glossary/access-token"><strong>An access token</strong></a> from your account. You will use an access token to associate a map with your account. Your access token is on the  <a href="https://www.mapbox.com/account/" rel="nofollow">Account page</a>.</p>
</li>
<li>
<p><a href="https://www.mapbox.com/mapbox-gl-js/" rel="nofollow"><strong>Mapbox GL JS</strong></a>. The Mapbox JavaScript library that uses WebGL to render interactive maps from Mapbox GL styles.</p>
</li>
<li>
<p><strong>A text editor.</strong> You'll be writing HTML, CSS, and JavaScript after all.</p>
</li>
<li>
<p><strong>Data</strong>. We collected some of Sweetgreen's locations and marked up the data in GeoJSON.</p>
</li>
<li>
<p><strong>Custom map marker</strong>. You'll be using an image for your map marker. Save the image to your project folder.</p>
</li>
</ul>
<p>{{
&lt;Button href="/help/demos/store-locator/marker.png" passthroughProps={{ download: "marker" }} &gt;
 Download custom marker

}}</p>
<h2><a id="user-content-add-structure" class="anchor" aria-hidden="true" href="#add-structure"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add structure</h2>
<p>In your project folder, create an <code>index.html</code> file. Set up the document by adding Mapbox GL JS and CSS to your <code>head</code>:</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;
&lt;<span class="pl-ent">link</span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css<span class="pl-pds">'</span></span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">'</span>stylesheet<span class="pl-pds">'</span></span> /&gt;</pre></div>
<p>Next, markup the page to create a map container and sidebar listing:</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">'</span>sidebar pad2<span class="pl-pds">'</span></span>&gt;Listing&lt;/<span class="pl-ent">div</span>&gt;
&lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">'</span>map pad2<span class="pl-pds">'</span></span>&gt;Map&lt;/<span class="pl-ent">div</span>&gt;</pre></div>
<p>Then, apply some CSS to create the page layout:</p>
<div class="highlight highlight-source-css"><pre><span class="pl-ent">body</span> {
  <span class="pl-c1"><span class="pl-c1">background</span></span>: <span class="pl-c1">#404040</span>;
  <span class="pl-c1"><span class="pl-c1">color</span></span>: <span class="pl-c1">#f8f8f8</span>;
  <span class="pl-c1"><span class="pl-c1">font</span></span>: <span class="pl-c1">500</span> <span class="pl-c1">20<span class="pl-k">px</span></span>/<span class="pl-c1">26<span class="pl-k">px</span></span> <span class="pl-s"><span class="pl-pds">'</span>Helvetica Neue<span class="pl-pds">'</span></span>, <span class="pl-c1">Helvetica</span>, <span class="pl-c1">Arial</span>, <span class="pl-c1">Sans-serif</span>;
  <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">-webkit-font-smoothing</span></span>: <span class="pl-c1">antialiased</span>;
}

<span class="pl-c"><span class="pl-c">/*</span> The page is split between map and sidebar - the sidebar gets 1/3, map</span>
<span class="pl-c">gets 2/3 of the page. You can adjust this to your personal liking. <span class="pl-c">*/</span></span>
<span class="pl-e">.sidebar</span> {
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">33.3333<span class="pl-k">%</span></span>;
}

<span class="pl-e">.map</span> {
  <span class="pl-c1"><span class="pl-c1">border-left</span></span>: <span class="pl-c1">1<span class="pl-k">px</span></span> <span class="pl-c1">solid</span> <span class="pl-c1">#fff</span>;
  <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;
  <span class="pl-c1"><span class="pl-c1">left</span></span>: <span class="pl-c1">33.3333<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">66.6666<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">bottom</span></span>: <span class="pl-c1">0</span>;
}

<span class="pl-e">.pad2</span> {
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">-webkit-box-sizing</span></span>: <span class="pl-c1">border-box</span>;
  <span class="pl-c1"><span class="pl-c1">-moz-box-sizing</span></span>: <span class="pl-c1">border-box</span>;
  <span class="pl-c1"><span class="pl-c1">box-sizing</span></span>: <span class="pl-c1">border-box</span>;
}</pre></div>
<p>{{

}}</p>
<h2><a id="user-content-initialize-the-map" class="anchor" aria-hidden="true" href="#initialize-the-map"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Initialize the map</h2>
<p>Now that you have the structure of the page, initialize the map with Mapbox GL JS.</p>
<p>First, add your access token using <code>mapboxgl.accessToken</code>. Then, create a new <code>map</code> object using <code>new mapboxgl.Map()</code> and store it in a variable called <code>map</code>:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>{{ &lt;UserAccessToken /&gt; }}<span class="pl-pds">'</span></span>;
<span class="pl-c"><span class="pl-c">//</span> This adds the map to your page</span>
<span class="pl-k">var</span> map <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">mapboxgl.Map</span>({
  <span class="pl-c"><span class="pl-c">//</span> container id specified in the HTML</span>
  container<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span>,
  <span class="pl-c"><span class="pl-c">//</span> style URL</span>
  style<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}<span class="pl-pds">'</span></span>,
  <span class="pl-c"><span class="pl-c">//</span> initial position in [lon, lat] format</span>
  center<span class="pl-k">:</span> [<span class="pl-k">-</span><span class="pl-c1">77.034084</span>, <span class="pl-c1">38.909671</span>],
  <span class="pl-c"><span class="pl-c">//</span> initial zoom</span>
  zoom<span class="pl-k">:</span> <span class="pl-c1">14</span>
});</pre></div>
<p>As you can see above, the Mapbox GL JS map requires several options:</p>
<ul>
<li>
<p><code>container</code>: the <code>id</code> of the <code>&lt;div&gt;</code> element on the page where the map should live. In this case, the <code>id</code> for the <code>&lt;div&gt;</code> is <code>'map'</code>.</p>
</li>
<li>
<p><code>style</code>: the <a href="/mapbox/help/blob/publisher-production/help/glossary/style-url">style URL</a> for the map style. In this case, use the {{  }} which has the style URL <code>mapbox://styles/mapbox/light-{{constants.VERSION_LIGHT_STYLE}}</code>.</p>
</li>
<li>
<p><code>center</code>: the initial centerpoint of the map in [longitude, latitude] format.</p>
</li>
<li>
<p><code>zoom</code>: the initial zoom level of the map.</p>
</li>
</ul>
<h2><a id="user-content-load-data" class="anchor" aria-hidden="true" href="#load-data"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Load data</h2>
<p>With Mapbox GL JS, map rendering happens in the browser. For the browser to render your map, you need to add a layer with geospatial data and instructions for how that data should be rendered.</p>
<p>To add a source to the map, your code needs to access the geospatial data. Store all the GeoJSON data in <code>sweetgreen.geojson</code> in a variable called <code>stores</code>:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> stores <span class="pl-k">=</span> {{ sweetgreenLocations }};</pre></div>
<p>Now you can add a layer that contains this data and describes how it should be rendered. Add the data to your map once the map loads using <code>addLayer()</code>. Create a new layer, and specify <code>stores</code> as a GeoJSON data source. Then, add instructions for rendering the source. This example only adds minimal styling --- for full details on all the layer styling options, see the <a href="https://www.mapbox.com/mapbox-gl-style-spec/" rel="nofollow">Mapbox Style Specification</a>:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>load<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>(<span class="pl-smi">e</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Add the data to your map as a layer</span>
  <span class="pl-smi">map</span>.<span class="pl-en">addLayer</span>({
    id<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>locations<span class="pl-pds">'</span></span>,
    type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>symbol<span class="pl-pds">'</span></span>,
    <span class="pl-c"><span class="pl-c">//</span> Add a GeoJSON source containing place coordinates and information.</span>
    source<span class="pl-k">:</span> {
      type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>geojson<span class="pl-pds">'</span></span>,
      data<span class="pl-k">:</span> stores
    },
    layout<span class="pl-k">:</span> {
      <span class="pl-s"><span class="pl-pds">'</span>icon-image<span class="pl-pds">'</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>restaurant-15<span class="pl-pds">'</span></span>,
      <span class="pl-s"><span class="pl-pds">'</span>icon-allow-overlap<span class="pl-pds">'</span></span><span class="pl-k">:</span> <span class="pl-c1">true</span>,
    }
  });
});</pre></div>
<p><em>Note: <code>restaurant-15</code> refers to an icon in the Mapbox Light style you added earlier in the code.</em></p>
<p>{{

}}</p>
<h2><a id="user-content-build-store-listing" class="anchor" aria-hidden="true" href="#build-store-listing"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Build store listing</h2>
<p>Now that the points are on your map, it's time to build the restaurant location listing by iterating through the GeoJSON and creating a list of restaurants dynamically. This means that if you need to add a location then you <em>only</em> need to update the GeoJSON.</p>
<p>First, update the sidebar HTML to hold the listing information and update your CSS to accommodate the layout changes:</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">'</span>sidebar<span class="pl-pds">'</span></span>&gt;
  &lt;<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">'</span>heading<span class="pl-pds">'</span></span>&gt;
    &lt;<span class="pl-ent">h1</span>&gt;Our locations&lt;/<span class="pl-ent">h1</span>&gt;
  &lt;/<span class="pl-ent">div</span>&gt;
  &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">'</span>listings<span class="pl-pds">'</span></span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">'</span>listings<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">div</span>&gt;
&lt;/<span class="pl-ent">div</span>&gt;</pre></div>
<div class="highlight highlight-source-css"><pre><span class="pl-ent">body</span> {
  <span class="pl-c1"><span class="pl-c1">color</span></span>: <span class="pl-c1">#404040</span>;
  <span class="pl-c1"><span class="pl-c1">font</span></span>: <span class="pl-c1">400</span> <span class="pl-c1">15<span class="pl-k">px</span></span>/<span class="pl-c1">22<span class="pl-k">px</span></span> <span class="pl-s"><span class="pl-pds">'</span>Source Sans Pro<span class="pl-pds">'</span></span>, <span class="pl-s"><span class="pl-pds">'</span>Helvetica Neue<span class="pl-pds">'</span></span>, <span class="pl-c1">Sans-serif</span>;
  <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">-webkit-font-smoothing</span></span>: <span class="pl-c1">antialiased</span>;
}

<span class="pl-ent">*</span> {
  <span class="pl-c1"><span class="pl-c1">-webkit-box-sizing</span></span>: <span class="pl-c1">border-box</span>;
  <span class="pl-c1"><span class="pl-c1">-moz-box-sizing</span></span>: <span class="pl-c1">border-box</span>;
  <span class="pl-c1"><span class="pl-c1">box-sizing</span></span>: <span class="pl-c1">border-box</span>;
}

<span class="pl-ent">h1</span> {
  <span class="pl-c1"><span class="pl-c1">font-size</span></span>: <span class="pl-c1">22<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">font-weight</span></span>: <span class="pl-c1">400</span>;
  <span class="pl-c1"><span class="pl-c1">line-height</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span> <span class="pl-c1">2<span class="pl-k">px</span></span>;
}

<span class="pl-ent">a</span> {
  <span class="pl-c1"><span class="pl-c1">color</span></span>: <span class="pl-c1">#404040</span>;
  <span class="pl-c1"><span class="pl-c1">text-decoration</span></span>: <span class="pl-c1">none</span>;
}

<span class="pl-ent">a</span><span class="pl-e">:hover</span> {
  <span class="pl-c1"><span class="pl-c1">color</span></span>: <span class="pl-c1">#101010</span>;
}

<span class="pl-e">.sidebar</span> {
  <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">33.3333<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">height</span></span>: <span class="pl-c1">100<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">left</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">overflow</span></span>: <span class="pl-c1">hidden</span>;
  <span class="pl-c1"><span class="pl-c1">border-right</span></span>: <span class="pl-c1">1<span class="pl-k">px</span></span> <span class="pl-c1">solid</span> <span class="pl-c1">rgba</span>(<span class="pl-c1">0</span>, <span class="pl-c1">0</span>, <span class="pl-c1">0</span>, <span class="pl-c1">0.25</span>);
}

<span class="pl-e">.pad2</span> {
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span>;
}

<span class="pl-e">.map</span> {
  <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;
  <span class="pl-c1"><span class="pl-c1">left</span></span>: <span class="pl-c1">33.3333<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">66.6666<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">bottom</span></span>: <span class="pl-c1">0</span>;
}

<span class="pl-e">.heading</span> {
  <span class="pl-c1"><span class="pl-c1">background</span></span>: <span class="pl-c1">#fff</span>;
  <span class="pl-c1"><span class="pl-c1">border-bottom</span></span>: <span class="pl-c1">1<span class="pl-k">px</span></span> <span class="pl-c1">solid</span> <span class="pl-c1">#eee</span>;
  <span class="pl-c1"><span class="pl-c1">height</span></span>: <span class="pl-c1">60<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">line-height</span></span>: <span class="pl-c1">60<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">0</span> <span class="pl-c1">10<span class="pl-k">px</span></span>;
}

<span class="pl-e">.listings</span> {
  <span class="pl-c1"><span class="pl-c1">height</span></span>: <span class="pl-c1">100<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">overflow</span></span>: <span class="pl-c1">auto</span>;
  <span class="pl-c1"><span class="pl-c1">padding-bottom</span></span>: <span class="pl-c1">60<span class="pl-k">px</span></span>;
}

<span class="pl-e">.listings</span> <span class="pl-e">.item</span> {
  <span class="pl-c1"><span class="pl-c1">display</span></span>: <span class="pl-c1">block</span>;
  <span class="pl-c1"><span class="pl-c1">border-bottom</span></span>: <span class="pl-c1">1<span class="pl-k">px</span></span> <span class="pl-c1">solid</span> <span class="pl-c1">#eee</span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">10<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">text-decoration</span></span>: <span class="pl-c1">none</span>;
}

<span class="pl-e">.listings</span> <span class="pl-e">.item</span><span class="pl-e">:last-child</span> { <span class="pl-c1"><span class="pl-c1">border-bottom</span></span>: <span class="pl-c1">none</span>; }

<span class="pl-e">.listings</span> <span class="pl-e">.item</span> <span class="pl-e">.title</span> {
  <span class="pl-c1"><span class="pl-c1">display</span></span>: <span class="pl-c1">block</span>;
  <span class="pl-c1"><span class="pl-c1">color</span></span>: <span class="pl-c1">#00853e</span>;
  <span class="pl-c1"><span class="pl-c1">font-weight</span></span>: <span class="pl-c1">700</span>;
}

<span class="pl-e">.listings</span> <span class="pl-e">.item</span> <span class="pl-e">.title</span> <span class="pl-ent">small</span> { <span class="pl-c1"><span class="pl-c1">font-weight</span></span>: <span class="pl-c1">400</span>; }

<span class="pl-e">.listings</span> <span class="pl-e">.item.active</span> <span class="pl-e">.title</span>,
<span class="pl-e">.listings</span> <span class="pl-e">.item</span> <span class="pl-e">.title</span><span class="pl-e">:hover</span> { <span class="pl-c1"><span class="pl-c1">color</span></span>: <span class="pl-c1">#8cc63f</span>; }

<span class="pl-e">.listings</span> <span class="pl-e">.item.active</span> {
  <span class="pl-c1"><span class="pl-c1">background-color</span></span>: <span class="pl-c1">#f8f8f8</span>;
}

<span class="pl-e">::-webkit-scrollbar</span> {
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">3<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">height</span></span>: <span class="pl-c1">3<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">border-left</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">background</span></span>: <span class="pl-c1">rgba</span>(<span class="pl-c1">0</span>, <span class="pl-c1">0</span>, <span class="pl-c1">0</span>, <span class="pl-c1">0.1</span>);
}

<span class="pl-e">::-webkit-scrollbar-track</span> {
  <span class="pl-c1"><span class="pl-c1">background</span></span>: <span class="pl-c1">none</span>;
}

<span class="pl-e">::-webkit-scrollbar-thumb</span> {
  <span class="pl-c1"><span class="pl-c1">background</span></span>: <span class="pl-c1">#00853e</span>;
  <span class="pl-c1"><span class="pl-c1">border-radius</span></span>: <span class="pl-c1">0</span>;
}

<span class="pl-e">.clearfix</span> { <span class="pl-c1"><span class="pl-c1">display</span></span>: <span class="pl-c1">block</span>; }

<span class="pl-e">.clearfix</span><span class="pl-e">::after</span> {
  <span class="pl-c1"><span class="pl-c1">content</span></span>: <span class="pl-s"><span class="pl-pds">'</span>.<span class="pl-pds">'</span></span>;
  <span class="pl-c1"><span class="pl-c1">display</span></span>: <span class="pl-c1">block</span>;
  <span class="pl-c1"><span class="pl-c1">height</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">clear</span></span>: <span class="pl-c1">both</span>;
  <span class="pl-c1"><span class="pl-c1">visibility</span></span>: <span class="pl-c1">hidden</span>;
}</pre></div>
<p>Next, build a function to iterate through the Sweetgreen locations and add each one to the sidebar listing:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">buildLocationList</span>(<span class="pl-smi">data</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Iterate through the list of stores</span>
  <span class="pl-k">for</span> (i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k">&lt;</span> <span class="pl-smi">data</span>.<span class="pl-smi">features</span>.<span class="pl-c1">length</span>; i<span class="pl-k">++</span>) {
    <span class="pl-k">var</span> currentFeature <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">features</span>[i];
    <span class="pl-c"><span class="pl-c">//</span> Shorten data.feature.properties to `prop` so we're not</span>
    <span class="pl-c"><span class="pl-c">//</span> writing this long form over and over again.</span>
    <span class="pl-k">var</span> prop <span class="pl-k">=</span> <span class="pl-smi">currentFeature</span>.<span class="pl-smi">properties</span>;
    <span class="pl-c"><span class="pl-c">//</span> Select the listing container in the HTML and append a div</span>
    <span class="pl-c"><span class="pl-c">//</span> with the class 'item' for each store</span>
    <span class="pl-k">var</span> listings <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementById</span>(<span class="pl-s"><span class="pl-pds">'</span>listings<span class="pl-pds">'</span></span>);
    <span class="pl-k">var</span> listing <span class="pl-k">=</span> <span class="pl-smi">listings</span>.<span class="pl-c1">appendChild</span>(<span class="pl-c1">document</span>.<span class="pl-c1">createElement</span>(<span class="pl-s"><span class="pl-pds">'</span>div<span class="pl-pds">'</span></span>));
    <span class="pl-smi">listing</span>.<span class="pl-c1">className</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>item<span class="pl-pds">'</span></span>;
    <span class="pl-smi">listing</span>.<span class="pl-c1">id</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>listing-<span class="pl-pds">'</span></span> <span class="pl-k">+</span> i;

    <span class="pl-c"><span class="pl-c">//</span> Create a new link with the class 'title' for each store</span>
    <span class="pl-c"><span class="pl-c">//</span> and fill it with the store address</span>
    <span class="pl-k">var</span> link <span class="pl-k">=</span> <span class="pl-smi">listing</span>.<span class="pl-c1">appendChild</span>(<span class="pl-c1">document</span>.<span class="pl-c1">createElement</span>(<span class="pl-s"><span class="pl-pds">'</span>a<span class="pl-pds">'</span></span>));
    <span class="pl-smi">link</span>.<span class="pl-c1">href</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>#<span class="pl-pds">'</span></span>;
    <span class="pl-smi">link</span>.<span class="pl-c1">className</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>title<span class="pl-pds">'</span></span>;
    <span class="pl-smi">link</span>.<span class="pl-smi">dataPosition</span> <span class="pl-k">=</span> i;
    <span class="pl-smi">link</span>.<span class="pl-smi">innerHTML</span> <span class="pl-k">=</span> <span class="pl-smi">prop</span>.<span class="pl-smi">address</span>;

    <span class="pl-c"><span class="pl-c">//</span> Create a new div with the class 'details' for each store</span>
    <span class="pl-c"><span class="pl-c">//</span> and fill it with the city and phone number</span>
    <span class="pl-k">var</span> details <span class="pl-k">=</span> <span class="pl-smi">listing</span>.<span class="pl-c1">appendChild</span>(<span class="pl-c1">document</span>.<span class="pl-c1">createElement</span>(<span class="pl-s"><span class="pl-pds">'</span>div<span class="pl-pds">'</span></span>));
    <span class="pl-smi">details</span>.<span class="pl-smi">innerHTML</span> <span class="pl-k">=</span> <span class="pl-smi">prop</span>.<span class="pl-smi">city</span>;
    <span class="pl-k">if</span> (<span class="pl-smi">prop</span>.<span class="pl-smi">phone</span>) {
      <span class="pl-smi">details</span>.<span class="pl-smi">innerHTML</span> <span class="pl-k">+=</span> <span class="pl-s"><span class="pl-pds">'</span> &amp;middot; <span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-smi">prop</span>.<span class="pl-smi">phoneFormatted</span>;
    }
  }
}</pre></div>
<p>Then, you will need to call this function when the map loads. You can do this by adding <code>buildLocationList(stores);</code> inside your <code>map.on('load', ...)</code> function after <code>addLayer()</code>. The result will look like this:</p>
<p>{{

}}</p>
<h2><a id="user-content-make-the-map-interactive" class="anchor" aria-hidden="true" href="#make-the-map-interactive"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Make the map interactive</h2>
<p>When a user clicks a link in the sidebar or on a point on the map, you want three things to happen:</p>
<ol>
<li>The map to fly to the associated store location.</li>
<li>A popup to be displayed at that point.</li>
<li>The listing to be highlighted in the sidebar.</li>
</ol>
<p>This will require a bit more code, but you can do it!</p>
<h3><a id="user-content-define-interactivity-functions" class="anchor" aria-hidden="true" href="#define-interactivity-functions"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Define interactivity functions</h3>
<p>First, define two functions: one that flies the map to the correct store, and one that displays a popup at that point. These functions will be fired both when a user clicks on a link in the sidebar listing and when a user clicks on a store location in the map. (Highlighting the listing on the sidebar will be handled separately for the two different click events.)</p>
<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">flyToStore</span>(<span class="pl-smi">currentFeature</span>) {
  <span class="pl-smi">map</span>.<span class="pl-en">flyTo</span>({
    center<span class="pl-k">:</span> <span class="pl-smi">currentFeature</span>.<span class="pl-smi">geometry</span>.<span class="pl-smi">coordinates</span>,
    zoom<span class="pl-k">:</span> <span class="pl-c1">15</span>
  });
}

<span class="pl-k">function</span> <span class="pl-en">createPopUp</span>(<span class="pl-smi">currentFeature</span>) {
  <span class="pl-k">var</span> popUps <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementsByClassName</span>(<span class="pl-s"><span class="pl-pds">'</span>mapboxgl-popup<span class="pl-pds">'</span></span>);
  <span class="pl-c"><span class="pl-c">//</span> Check if there is already a popup on the map and if so, remove it</span>
  <span class="pl-k">if</span> (popUps[<span class="pl-c1">0</span>]) popUps[<span class="pl-c1">0</span>].<span class="pl-c1">remove</span>();

  <span class="pl-k">var</span> popup <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">mapboxgl.Popup</span>({ closeOnClick<span class="pl-k">:</span> <span class="pl-c1">false</span> })
    .<span class="pl-en">setLngLat</span>(<span class="pl-smi">currentFeature</span>.<span class="pl-smi">geometry</span>.<span class="pl-smi">coordinates</span>)
    .<span class="pl-en">setHTML</span>(<span class="pl-s"><span class="pl-pds">'</span>&lt;h3&gt;Sweetgreen&lt;/h3&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span>
      <span class="pl-s"><span class="pl-pds">'</span>&lt;h4&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-smi">currentFeature</span>.<span class="pl-smi">properties</span>.<span class="pl-smi">address</span> <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;/h4&gt;<span class="pl-pds">'</span></span>)
    .<span class="pl-en">addTo</span>(map);
}</pre></div>
<p>You can also style your popups using CSS:</p>
<div class="highlight highlight-source-css"><pre><span class="pl-c"><span class="pl-c">/*</span> Marker tweaks <span class="pl-c">*/</span></span>
<span class="pl-e">.mapboxgl-popup-close-button</span> {
  <span class="pl-c1"><span class="pl-c1">display</span></span>: <span class="pl-c1">none</span>;
}

<span class="pl-e">.mapboxgl-popup-content</span> {
  <span class="pl-c1"><span class="pl-c1">font</span></span>: <span class="pl-c1">400</span> <span class="pl-c1">15<span class="pl-k">px</span></span>/<span class="pl-c1">22<span class="pl-k">px</span></span> <span class="pl-s"><span class="pl-pds">'</span>Source Sans Pro<span class="pl-pds">'</span></span>, <span class="pl-s"><span class="pl-pds">'</span>Helvetica Neue<span class="pl-pds">'</span></span>, <span class="pl-c1">Sans-serif</span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">180<span class="pl-k">px</span></span>;
}

<span class="pl-e">.mapboxgl-popup-content-wrapper</span> {
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">1<span class="pl-k">%</span></span>;
}

<span class="pl-e">.mapboxgl-popup-content</span> <span class="pl-ent">h3</span> {
  <span class="pl-c1"><span class="pl-c1">background</span></span>: <span class="pl-c1">#91c949</span>;
  <span class="pl-c1"><span class="pl-c1">color</span></span>: <span class="pl-c1">#fff</span>;
  <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">display</span></span>: <span class="pl-c1">block</span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">10<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">border-radius</span></span>: <span class="pl-c1">3<span class="pl-k">px</span></span> <span class="pl-c1">3<span class="pl-k">px</span></span> <span class="pl-c1">0</span> <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">font-weight</span></span>: <span class="pl-c1">700</span>;
  <span class="pl-c1"><span class="pl-c1">margin-top</span></span>: <span class="pl-c1">-15<span class="pl-k">px</span></span>;
}

<span class="pl-e">.mapboxgl-popup-content</span> <span class="pl-ent">h4</span> {
  <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">display</span></span>: <span class="pl-c1">block</span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">10<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">font-weight</span></span>: <span class="pl-c1">400</span>;
}

<span class="pl-e">.mapboxgl-popup-content</span> <span class="pl-ent">div</span> {
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">10<span class="pl-k">px</span></span>;
}

<span class="pl-e">.mapboxgl-container</span> <span class="pl-e">.leaflet-marker-icon</span> {
  <span class="pl-c1"><span class="pl-c1">cursor</span></span>: <span class="pl-c1">pointer</span>;
}

<span class="pl-e">.mapboxgl-popup-anchor-top</span> <span class="pl-k">&gt;</span> <span class="pl-e">.mapboxgl-popup-content</span> {
  <span class="pl-c1"><span class="pl-c1">margin-top</span></span>: <span class="pl-c1">15<span class="pl-k">px</span></span>;
}

<span class="pl-e">.mapboxgl-popup-anchor-top</span> <span class="pl-k">&gt;</span> <span class="pl-e">.mapboxgl-popup-tip</span> {
  <span class="pl-c1"><span class="pl-c1">border-bottom-color</span></span>: <span class="pl-c1">#91c949</span>;
}</pre></div>
<p>For the <code>.remove()</code> method to work in older browsers, you will need to include the code below at the beginning of your script:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> This will let you use the .remove() function later on</span>
<span class="pl-k">if</span> (<span class="pl-k">!</span>(<span class="pl-s"><span class="pl-pds">'</span>remove<span class="pl-pds">'</span></span> <span class="pl-k">in</span> <span class="pl-c1">Element</span>.<span class="pl-c1">prototype</span>)) {
  <span class="pl-c1">Element</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">remove</span> <span class="pl-k">=</span> <span class="pl-k">function</span>() {
    <span class="pl-k">if</span> (<span class="pl-c1">this</span>.<span class="pl-c1">parentNode</span>) {
      <span class="pl-c1">this</span>.<span class="pl-c1">parentNode</span>.<span class="pl-c1">removeChild</span>(<span class="pl-c1">this</span>);
    }
  };
}</pre></div>
<p>See the <a href="https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove" rel="nofollow">HTML documentation</a> for more information.</p>
<h3><a id="user-content-add-event-listeners" class="anchor" aria-hidden="true" href="#add-event-listeners"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add event listeners</h3>
<p>Now that you've defined these two functions, you want them to fire when a user clicks on a restaurant in the sidebar listing or when a user clicks on a restaurant on the map. To do this, you will add <em>event listeners</em> that listen for "click" events and execute some function when they happen. You will add two event listeners: one for when a link in the sidebar is clicked and one for when a location on the map is clicked.</p>
<p>Use this code for when a link is clicked:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> Add an event listener for the links in the sidebar listing</span>
<span class="pl-smi">link</span>.<span class="pl-c1">addEventListener</span>(<span class="pl-s"><span class="pl-pds">'</span>click<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>(<span class="pl-smi">e</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Update the currentFeature to the store associated with the clicked link</span>
  <span class="pl-k">var</span> clickedListing <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">features</span>[<span class="pl-c1">this</span>.<span class="pl-smi">dataPosition</span>];
  <span class="pl-c"><span class="pl-c">//</span> 1. Fly to the point associated with the clicked link</span>
  <span class="pl-en">flyToStore</span>(clickedListing);
  <span class="pl-c"><span class="pl-c">//</span> 2. Close all other popups and display popup for clicked store</span>
  <span class="pl-en">createPopUp</span>(clickedListing);
  <span class="pl-c"><span class="pl-c">//</span> 3. Highlight listing in sidebar (and remove highlight for all other listings)</span>
  <span class="pl-k">var</span> activeItem <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementsByClassName</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
  <span class="pl-k">if</span> (activeItem[<span class="pl-c1">0</span>]) {
    activeItem[<span class="pl-c1">0</span>].<span class="pl-smi">classList</span>.<span class="pl-c1">remove</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
  }
  <span class="pl-c1">this</span>.<span class="pl-c1">parentNode</span>.<span class="pl-smi">classList</span>.<span class="pl-c1">add</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
});</pre></div>
<p>Use this code for when a location on the map is clicked:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> Add an event listener for when a user clicks on the map</span>
<span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>click<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>(<span class="pl-smi">e</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Query all the rendered points in the view</span>
  <span class="pl-k">var</span> features <span class="pl-k">=</span> <span class="pl-smi">map</span>.<span class="pl-en">queryRenderedFeatures</span>(<span class="pl-smi">e</span>.<span class="pl-smi">point</span>, { layers<span class="pl-k">:</span> [<span class="pl-s"><span class="pl-pds">'</span>locations<span class="pl-pds">'</span></span>] });
  <span class="pl-k">if</span> (<span class="pl-smi">features</span>.<span class="pl-c1">length</span>) {
    <span class="pl-k">var</span> clickedPoint <span class="pl-k">=</span> features[<span class="pl-c1">0</span>];
    <span class="pl-c"><span class="pl-c">//</span> 1. Fly to the point</span>
    <span class="pl-en">flyToStore</span>(clickedPoint);
    <span class="pl-c"><span class="pl-c">//</span> 2. Close all other popups and display popup for clicked store</span>
    <span class="pl-en">createPopUp</span>(clickedPoint);
    <span class="pl-c"><span class="pl-c">//</span> 3. Highlight listing in sidebar (and remove highlight for all other listings)</span>
    <span class="pl-k">var</span> activeItem <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementsByClassName</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
    <span class="pl-k">if</span> (activeItem[<span class="pl-c1">0</span>]) {
      activeItem[<span class="pl-c1">0</span>].<span class="pl-smi">classList</span>.<span class="pl-c1">remove</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
    }
    <span class="pl-c"><span class="pl-c">//</span> Find the index of the store.features that corresponds to the clickedPoint that fired the event listener</span>
    <span class="pl-k">var</span> selectedFeature <span class="pl-k">=</span> <span class="pl-smi">clickedPoint</span>.<span class="pl-smi">properties</span>.<span class="pl-smi">address</span>;

    <span class="pl-k">for</span> (<span class="pl-k">var</span> i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k">&lt;</span> <span class="pl-smi">stores</span>.<span class="pl-smi">features</span>.<span class="pl-c1">length</span>; i<span class="pl-k">++</span>) {
      <span class="pl-k">if</span> (<span class="pl-smi">stores</span>.<span class="pl-smi">features</span>[i].<span class="pl-smi">properties</span>.<span class="pl-smi">address</span> <span class="pl-k">===</span> selectedFeature) {
        selectedFeatureIndex <span class="pl-k">=</span> i;
      }
    }
    <span class="pl-c"><span class="pl-c">//</span> Select the correct list item using the found index and add the active class</span>
    <span class="pl-k">var</span> listing <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementById</span>(<span class="pl-s"><span class="pl-pds">'</span>listing-<span class="pl-pds">'</span></span> <span class="pl-k">+</span> selectedFeatureIndex);
    <span class="pl-smi">listing</span>.<span class="pl-smi">classList</span>.<span class="pl-c1">add</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
  }
});</pre></div>
<p>{{

}}</p>
<h2><a id="user-content-add-custom-markers" class="anchor" aria-hidden="true" href="#add-custom-markers"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add custom markers</h2>
<p>This section will walk you through how to replace the existing standard symbol layer with custom markers. First, you will need to remove the existing symbol layer and related functions. Remove the symbol layer by deleting the <code>.addLayer()</code> function from your code, and replace it with the <code>.addSource()</code> code below. Instead of styling the symbol layer with <code>addLayer</code>, you will use the Markers API to add an image to each point in the GeoJSON data:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">map</span>.<span class="pl-en">addSource</span>(<span class="pl-s"><span class="pl-pds">'</span>places<span class="pl-pds">'</span></span>, {
  type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>geojson<span class="pl-pds">'</span></span>,
  data<span class="pl-k">:</span> stores
});</pre></div>
<p>You'll also want to delete the <a href="#symbol-click">function that listened for a click on a symbol</a> to fly to the location, display a popup, and highlight the list item. Then, add the custom Sweetgreen icons to the map using <code>mapboxgl.Marker()</code> objects. Unlike the symbol layer, which has symbols embedded in the map, <code>mapboxgl.Marker()</code> objects are HTML DOM elements that can be styled with CSS. Add a new class to the CSS called <code>.marker</code> and set the Sweetgreen marker you <a href="/mapbox/help/blob/publisher-production/help/demos/store-locator/marker.png">downloaded</a> earlier as the <code>background-image</code>:</p>
<div class="highlight highlight-source-css"><pre><span class="pl-e">.marker</span> {
  <span class="pl-c1"><span class="pl-c1">border</span></span>: <span class="pl-c1">none</span>;
  <span class="pl-c1"><span class="pl-c1">cursor</span></span>: <span class="pl-c1">pointer</span>;
  <span class="pl-c1"><span class="pl-c1">height</span></span>: <span class="pl-c1">56<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">56<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">background-image</span></span>: <span class="pl-c1">url</span>(<span class="pl-v">marker.png</span>);
  <span class="pl-c1"><span class="pl-c1">background-color</span></span>: <span class="pl-c1">rgba</span>(<span class="pl-c1">0</span>, <span class="pl-c1">0</span>, <span class="pl-c1">0</span>, <span class="pl-c1">0</span>);
}</pre></div>
<p>To add the new markers to the map, iterate through all stores and add the new marker to the map at each location:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">stores</span>.<span class="pl-smi">features</span>.<span class="pl-c1">forEach</span>(<span class="pl-k">function</span>(<span class="pl-smi">marker</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Create a div element for the marker</span>
  <span class="pl-k">var</span> el <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">createElement</span>(<span class="pl-s"><span class="pl-pds">'</span>div<span class="pl-pds">'</span></span>);
  <span class="pl-c"><span class="pl-c">//</span> Add a class called 'marker' to each div</span>
  <span class="pl-smi">el</span>.<span class="pl-c1">className</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>marker<span class="pl-pds">'</span></span>;
  <span class="pl-c"><span class="pl-c">//</span> By default the image for your custom marker will be anchored</span>
  <span class="pl-c"><span class="pl-c">//</span> by its center. Adjust the position accordingly</span>
  <span class="pl-c"><span class="pl-c">//</span> Create the custom markers, set their position, and add to map</span>
  <span class="pl-k">new</span> <span class="pl-en">mapboxgl.Marker</span>(el, { offset<span class="pl-k">:</span> [<span class="pl-c1">0</span>, <span class="pl-k">-</span><span class="pl-c1">23</span>] })
    .<span class="pl-en">setLngLat</span>(<span class="pl-smi">marker</span>.<span class="pl-smi">geometry</span>.<span class="pl-smi">coordinates</span>)
    .<span class="pl-en">addTo</span>(map);
});</pre></div>
<h3><a id="user-content-add-new-event-listeners" class="anchor" aria-hidden="true" href="#add-new-event-listeners"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add new event listeners</h3>
<p>Now that you have replaced your symbols with markers, you will need to re-add some code for flying to the position on the map, displaying a popup, and highlighting the <code>list</code> item in the sidebar when clicking on the marker. Within your <code>forEach</code> function from above, add an event listener:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">el</span>.<span class="pl-c1">addEventListener</span>(<span class="pl-s"><span class="pl-pds">'</span>click<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>(<span class="pl-smi">e</span>) {
  <span class="pl-k">var</span> activeItem <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementsByClassName</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
  <span class="pl-c"><span class="pl-c">//</span> 1. Fly to the point</span>
  <span class="pl-en">flyToStore</span>(marker);
  <span class="pl-c"><span class="pl-c">//</span> 2. Close all other popups and display popup for clicked store</span>
  <span class="pl-en">createPopUp</span>(marker);
  <span class="pl-c"><span class="pl-c">//</span> 3. Highlight listing in sidebar (and remove highlight for all other listings)</span>
  <span class="pl-smi">e</span>.<span class="pl-c1">stopPropagation</span>();
  <span class="pl-k">if</span> (activeItem[<span class="pl-c1">0</span>]) {
    activeItem[<span class="pl-c1">0</span>].<span class="pl-smi">classList</span>.<span class="pl-c1">remove</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
  }
  <span class="pl-k">var</span> listing <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementById</span>(<span class="pl-s"><span class="pl-pds">'</span>listing-<span class="pl-pds">'</span></span> <span class="pl-k">+</span> i);
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(listing);
  <span class="pl-smi">listing</span>.<span class="pl-smi">classList</span>.<span class="pl-c1">add</span>(<span class="pl-s"><span class="pl-pds">'</span>active<span class="pl-pds">'</span></span>);
});</pre></div>
<h3><a id="user-content-final-tweaks" class="anchor" aria-hidden="true" href="#final-tweaks"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Final tweaks</h3>
<p>You will need to adjust the position of the popup to account for the added height of the marker. You can do this using CSS:</p>
<div class="highlight highlight-source-css"><pre><span class="pl-e">.mapboxgl-popup</span> {
  <span class="pl-c1"><span class="pl-c1">padding-bottom</span></span>: <span class="pl-c1">50<span class="pl-k">px</span></span>;
}</pre></div>
<p>At this point, you can also freshen up the type with Source Sans Pro:</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;<span class="pl-ent">link</span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">'</span>https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,700<span class="pl-pds">'</span></span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">'</span>stylesheet<span class="pl-pds">'</span></span>&gt;</pre></div>
<p>You'll need to update the <code>font</code> property in <code>body</code> style:</p>
<div class="highlight highlight-source-css"><pre><span class="pl-ent">font</span>: 400 15px/22px '<span class="pl-ent">Source</span> Sans Pro', 'Helvetica Neue', Sans-serif;</pre></div>
<h2><a id="user-content-finished-product" class="anchor" aria-hidden="true" href="#finished-product"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Finished product</h2>
<p>You have completed the store locator.</p>
<p>{{

}}</p>
<h2><a id="user-content-next-steps" class="anchor" aria-hidden="true" href="#next-steps"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Next steps</h2>
<p>After following this guide, you have the tools you need to create your own store locator. Explore more Mapbox GL JS resources on our <a href="/mapbox/help/blob/publisher-production/help/tutorials">help page</a>.</p>
</article>
  </div>

    </div>

  

  <details class="details-reset details-overlay details-overlay-dark">
    <summary data-hotkey="l" aria-label="Jump to line"></summary>
    <details-dialog class="Box Box--overlay d-flex flex-column anim-fade-in fast linejump" aria-label="Jump to line">
      <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="js-jump-to-line-form Box-body d-flex" action="" accept-charset="UTF-8" method="get"><input name="utf8" type="hidden" value="&#x2713;" />
        <input class="form-control flex-auto mr-3 linejump-input js-jump-to-line-field" type="text" placeholder="Jump to line&hellip;" aria-label="Jump to line" autofocus>
        <button type="submit" class="btn" data-close-dialog>Go</button>
</form>    </details-dialog>
  </details>



  </div>
</div>

    </main>
  </div>
  

  </div>

        
<div class="footer container-lg width-full p-responsive" role="contentinfo">
  <div class="position-relative d-flex flex-row-reverse flex-lg-row flex-wrap flex-lg-nowrap flex-justify-center flex-lg-justify-between pt-6 pb-2 mt-6 f6 text-gray border-top border-gray-light ">
    <ul class="list-style-none d-flex flex-wrap col-12 col-lg-5 flex-justify-center flex-lg-justify-between mb-2 mb-lg-0">
      <li class="mr-3 mr-lg-0">&copy; 2019 <span title="0.45324s from unicorn-74cfd9bd7b-4k78h">GitHub</span>, Inc.</li>
        <li class="mr-3 mr-lg-0"><a data-ga-click="Footer, go to terms, text:terms" href="https://github.com/site/terms">Terms</a></li>
        <li class="mr-3 mr-lg-0"><a data-ga-click="Footer, go to privacy, text:privacy" href="https://github.com/site/privacy">Privacy</a></li>
        <li class="mr-3 mr-lg-0"><a data-ga-click="Footer, go to security, text:security" href="https://github.com/security">Security</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://githubstatus.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
        <li><a data-ga-click="Footer, go to help, text:help" href="https://help.github.com">Help</a></li>
    </ul>

    <a aria-label="Homepage" title="GitHub" class="footer-octicon d-none d-lg-block mx-lg-4" href="https://github.com">
      <svg height="24" class="octicon octicon-mark-github" viewBox="0 0 16 16" version="1.1" width="24" aria-hidden="true"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
</a>
   <ul class="list-style-none d-flex flex-wrap col-12 col-lg-5 flex-justify-center flex-lg-justify-between mb-2 mb-lg-0">
        <li class="mr-3 mr-lg-0"><a data-ga-click="Footer, go to contact, text:contact" href="https://github.com/contact">Contact GitHub</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://github.com/pricing" data-ga-click="Footer, go to Pricing, text:Pricing">Pricing</a></li>
      <li class="mr-3 mr-lg-0"><a href="https://developer.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li class="mr-3 mr-lg-0"><a href="https://training.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://github.blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a data-ga-click="Footer, go to about, text:about" href="https://github.com/about">About</a></li>

    </ul>
  </div>
  <div class="d-flex flex-justify-center pb-6">
    <span class="f6 text-gray-light"></span>
  </div>
</div>



  <div id="ajax-error-message" class="ajax-error-message flash flash-error">
    <svg class="octicon octicon-alert" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8.893 1.5c-.183-.31-.52-.5-.887-.5s-.703.19-.886.5L.138 13.499a.98.98 0 0 0 0 1.001c.193.31.53.501.886.501h13.964c.367 0 .704-.19.877-.5a1.03 1.03 0 0 0 .01-1.002L8.893 1.5zm.133 11.497H6.987v-2.003h2.039v2.003zm0-3.004H6.987V5.987h2.039v4.006z"/></svg>
    <button type="button" class="flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
      <svg class="octicon octicon-x" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48L7.48 8z"/></svg>
    </button>
    You can’t perform that action at this time.
  </div>


    
    <script crossorigin="anonymous" integrity="sha512-jhsyFUjPFC1LxOHjP/rZLWSj9har3Q4LQ3ya4lS9PpUiDnBfQ03O7jKykHoOhCqwJD03W8TLda4mfewo+Qxz1w==" type="application/javascript" src="https://github.githubassets.com/assets/frameworks-0fbde9bd.js"></script>
    
    <script crossorigin="anonymous" async="async" integrity="sha512-nJeXrE3n7mXhk2gr5fsk/59wjFiLcLWr4oZbYEm44dsOrx2MZf2rlzQ87pe1Qjytyk7DH3x/sib1g3O39ifX8A==" type="application/javascript" src="https://github.githubassets.com/assets/github-bootstrap-bab8f6ab.js"></script>
    
    
    
  <div class="js-stale-session-flash stale-session-flash flash flash-warn flash-banner" hidden
    >
    <svg class="octicon octicon-alert" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8.893 1.5c-.183-.31-.52-.5-.887-.5s-.703.19-.886.5L.138 13.499a.98.98 0 0 0 0 1.001c.193.31.53.501.886.501h13.964c.367 0 .704-.19.877-.5a1.03 1.03 0 0 0 .01-1.002L8.893 1.5zm.133 11.497H6.987v-2.003h2.039v2.003zm0-3.004H6.987V5.987h2.039v4.006z"/></svg>
    <span class="signed-in-tab-flash">You signed in with another tab or window. <a href="">Reload</a> to refresh your session.</span>
    <span class="signed-out-tab-flash">You signed out in another tab or window. <a href="">Reload</a> to refresh your session.</span>
  </div>
  <template id="site-details-dialog">
  <details class="details-reset details-overlay details-overlay-dark lh-default text-gray-dark hx_rsm" open>
    <summary role="button" aria-label="Close dialog"></summary>
    <details-dialog class="Box Box--overlay d-flex flex-column anim-fade-in fast hx_rsm-dialog hx_rsm-modal">
      <button class="Box-btn-octicon m-0 btn-octicon position-absolute right-0 top-0" type="button" aria-label="Close dialog" data-close-dialog>
        <svg class="octicon octicon-x" viewBox="0 0 12 16" version="1.1" width="12" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48L7.48 8z"/></svg>
      </button>
      <div class="octocat-spinner my-6 js-details-dialog-spinner"></div>
    </details-dialog>
  </details>
</template>

  <div class="Popover js-hovercard-content position-absolute" style="display: none; outline: none;" tabindex="0">
  <div class="Popover-message Popover-message--bottom-left Popover-message--large Box box-shadow-large" style="width:360px;">
  </div>
</div>

  <div aria-live="polite" class="js-global-screen-reader-notice sr-only"></div>

  </body>
</html>

