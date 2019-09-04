





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
  
  <title>help/make-a-heatmap-with-mapbox-gl-js.md at publisher-production · mapbox/help</title>
    <meta name="description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub.">
    <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
  <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
  <meta property="fb:app_id" content="1401488693436528">

    <meta name="twitter:image:src" content="https://avatars2.githubusercontent.com/u/600935?s=400&amp;v=4" /><meta name="twitter:site" content="@github" /><meta name="twitter:card" content="summary" /><meta name="twitter:title" content="mapbox/help" /><meta name="twitter:description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub." />
    <meta property="og:image" content="https://avatars2.githubusercontent.com/u/600935?s=400&amp;v=4" /><meta property="og:site_name" content="GitHub" /><meta property="og:type" content="object" /><meta property="og:title" content="mapbox/help" /><meta property="og:url" content="https://github.com/mapbox/help" /><meta property="og:description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub." />

  <link rel="assets" href="https://github.githubassets.com/">
  <link rel="web-socket" href="wss://live.github.com/_sockets/VjI6MzAyOTU4NTE3OmMwN2I5N2M0NGVmNWFiOTUwYzNmZmQ1ZjBlZWM4MDE4YjgzN2E1YzE0MDNkYjJkODczZGYzZjZhYjI5YmE3MGQ=--8d866c8de3a42592ed75510b2f3d306fba5ea00b">
  <meta name="pjax-timeout" content="1000">
  <link rel="sudo-modal" href="/sessions/sudo_modal">
  <meta name="request-id" content="3EA2:92F6:11CA5C:1AB537:5D7026E4" data-pjax-transient>


  <link rel="sso-modal" href="/orgs/mapbox/sso_modal" data-pjax-transient="true"></link><link rel="sso-session" href="/orgs/mapbox/sso_status.json" data-pjax-transient="true"></link><meta name="sso-expires-around" content="1567704602" data-pjax-transient="true"></meta>

  <meta name="selected-link" value="repo_source" data-pjax-transient>

      <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
    <meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-site-verification" content="GXs5KoUUkNCoaAZn7wPN-t01Pywp9M3sEjnt_3_ZWPc">

  <meta name="octolytics-host" content="collector.githubapp.com" /><meta name="octolytics-app-id" content="github" /><meta name="octolytics-event-url" content="https://collector.githubapp.com/github-external/browser_event" /><meta name="octolytics-dimension-request_id" content="3EA2:92F6:11CA5C:1AB537:5D7026E4" /><meta name="octolytics-dimension-region_edge" content="sea" /><meta name="octolytics-dimension-region_render" content="iad" /><meta name="octolytics-dimension-ga_id" content="" class="js-octo-ga-id" /><meta name="octolytics-dimension-visitor_id" content="2058165157458336909" /><meta name="octolytics-actor-id" content="18397640" /><meta name="octolytics-actor-login" content="Jing-flyloveyin" /><meta name="octolytics-actor-hash" content="c7be0e1b8bc813e56ceee222f4a1c9e2890774570591d5891573b62c21660107" />
<meta name="analytics-location" content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" />



    <meta name="google-analytics" content="UA-3769691-2">

  <meta class="js-ga-set" name="userId" content="a377d279e504cd9111bf6c4e502c8d97">

<meta class="js-ga-set" name="dimension1" content="Logged In">



  

      <meta name="hostname" content="github.com">
    <meta name="user-login" content="Jing-flyloveyin">

      <meta name="expected-hostname" content="github.com">
    <meta name="js-proxy-site-detection-payload" content="NzNiZjJkYTQ3NGJhMzAyYTVmMjQzMzM4MmVlNzMzNjlkM2JmODg0YmNiMTQ5YWI3MmQ3ZDRkOTI4MmVhMjVlN3x7InJlbW90ZV9hZGRyZXNzIjoiNDUuNzkuODMuODEiLCJyZXF1ZXN0X2lkIjoiM0VBMjo5MkY2OjExQ0E1QzoxQUI1Mzc6NUQ3MDI2RTQiLCJ0aW1lc3RhbXAiOjE1Njc2MzEwODIsImhvc3QiOiJnaXRodWIuY29tIn0=">

    <meta name="enabled-features" content="ACTIONS_V2_ON_MARKETPLACE,MARKETPLACE_FEATURED_BLOG_POSTS,MARKETPLACE_INVOICED_BILLING,MARKETPLACE_SOCIAL_PROOF_CUSTOMERS,MARKETPLACE_TRENDING_SOCIAL_PROOF,MARKETPLACE_RECOMMENDATIONS,MARKETPLACE_PENDING_INSTALLATIONS,NOTIFY_ON_BLOCK,RELATED_ISSUES,GHE_CLOUD_TRIAL">

  <meta name="html-safe-nonce" content="fb97dd135de80342fdc477688b418fc612fd0e7e">

  <meta http-equiv="x-pjax-version" content="785dc78f1f1353014e3eece9d3f39215">
  

      <link href="https://github.com/mapbox/help/commits/publisher-production.atom?token=AEMLTSHRHV2CKCLRXNRJKEN3PVTXU" rel="alternate" title="Recent Commits to help:publisher-production" type="application/atom+xml">

  <meta name="go-import" content="github.com/mapbox/help git https://github.com/mapbox/help.git">

  <meta name="octolytics-dimension-user_id" content="600935" /><meta name="octolytics-dimension-user_login" content="mapbox" /><meta name="octolytics-dimension-repository_id" content="34758294" /><meta name="octolytics-dimension-repository_nwo" content="mapbox/help" /><meta name="octolytics-dimension-repository_public" content="false" /><meta name="octolytics-dimension-repository_is_fork" content="false" /><meta name="octolytics-dimension-repository_network_root_id" content="34758294" /><meta name="octolytics-dimension-repository_network_root_nwo" content="mapbox/help" /><meta name="octolytics-dimension-repository_explore_github_marketplace_ci_cta_shown" content="false" />


    <link rel="canonical" href="https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md" data-pjax-transient>


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
          data-jump-to-suggestions-path="/_graphql/GetSuggestedNavigationDestinations#csrf-token=zCzmpG42F4JdjT1iZlkN2eDlAgGBAqqZZgGP4GwPPgZNhTvENt8kWS2oBxEAejvpvockZv0ZzdEq8tUQRWCQIA=="
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
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form action="/logout" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="GY2eflHQQMs/Sg3C2xjJ2oywW1KCuGJQ819U5CsRlPxdX6dFQyQWfJ2R5qaxaCVU48s3piFWd5MNfDnnMUuYXA==" />
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
      role="menuitem" data-hydro-click="{&quot;event_type&quot;:&quot;user_profile.click&quot;,&quot;payload&quot;:{&quot;profile_user_id&quot;:600935,&quot;target&quot;:&quot;EDIT_USER_STATUS&quot;,&quot;user_id&quot;:18397640,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;3EA2:92F6:11CA5C:1AB537:5D7026E4&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;}}" data-hydro-click-hmac="17c4038a8bf236bf3bf98ea316a90f355e7bbb8ce496fd09bf6ec9a9900a8683">
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
      <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="position-relative flex-auto js-user-status-form" action="/users/status?compact=1&amp;link_mentions=0&amp;truncate=1" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="_method" value="put" /><input type="hidden" name="authenticity_token" value="6KtHcp8SA/qXRFLph75qAZnDFhQVZdrcSLHGS+bkuQK/VtucVraMxVKAp+/EQAOo5rtZYdIepPRhPa2fXhYiEw==" />
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
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 30 minutes" value="2019-09-04T14:34:42-07:00">
            in 30 minutes
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 1 hour" value="2019-09-04T15:04:42-07:00">
            in 1 hour
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 4 hours" value="2019-09-04T18:04:42-07:00">
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
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="logout-form" action="/logout" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="pPHg1tpZ/DaYokmUKJZnVs1xSVDUKLNcAzqiRIMtIefgI9ntyK2qgTp5ovBC5ovYogolpHfGpp/9Gc9HmXctRw==" />
      
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
      <a class="btn btn-primary shelf-cta" target="_blank" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;READ_GUIDE&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;3EA2:92F6:11CA5C:1AB537:5D7026E4&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="e292cf9117a6aafbd4adfce98a1453817843001c318f5f17e9fa08c2491198c9" href="https://guides.github.com/activities/hello-world/">Read the guide</a>
    </div>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="shelf-dismiss js-notice-dismiss" action="/dashboard/dismiss_bootcamp" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="_method" value="delete" /><input type="hidden" name="authenticity_token" value="x3Y+DHeROQq/JpranUXJa76PqfcRnONCjHANiEtBnqb71NgV/wQ+9GMgqpXCq29VFq9aS+9cw4ac0Ot1Y93CEg==" />
      <button name="button" type="submit" class="mr-1 close-button tooltipped tooltipped-w" aria-label="Hide this notice forever" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;DISMISS_BANNER&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;3EA2:92F6:11CA5C:1AB537:5D7026E4&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="5a67f54f5c3c88ae57fa672cce94771c12cf47526cac3ce58887b9f93ccc61f2">
        <svg aria-label="Hide this notice forever" class="octicon octicon-x v-align-text-top" viewBox="0 0 12 16" version="1.1" width="12" height="16" role="img"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48L7.48 8z"/></svg>
</button></form>  </div>
</div>



  








  <div class="pagehead repohead instapaper_ignore readability-menu experiment-repo-nav pt-0 pt-lg-4 ">
    <div class="repohead-details-container clearfix container-lg p-responsive d-none d-lg-block">

      <ul class="pagehead-actions">




  <li>
    
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form data-remote="true" class="clearfix js-social-form js-social-container" action="/notifications/subscribe" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="NT4DTMoCnIDMaAtd/xkwLLKrIff4B42L6VSBmLCmQmSZRdxelcILYvEgp5XhDsC15iS0lDaP510XvQIa5CelFA==" />      <input type="hidden" name="repository_id" value="34758294">

      <details class="details-reset details-overlay select-menu float-left">
        <summary class="select-menu-button float-left btn btn-sm btn-with-count" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;WATCH_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;3EA2:92F6:11CA5C:1AB537:5D7026E4&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="73b41ccc9f3f89740165eb14a2f1fd134ac51e4e83281e8a1e4ced7101f3b567" data-ga-click="Repository, click Watch settings, action:blob#show">          <span data-menu-button>
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
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="starred js-social-form" action="/mapbox/help/unstar" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="Qv43o7IjV87WkKKjwqxScRZFQiDQDjBmVacBYmoE77AleNGKepu8n4YrTNjuNbTTWgEfhuft9gZk6rJ/jcigqw==" />
      <input type="hidden" name="context" value="repository"></input>
      <button type="submit" class="btn btn-sm btn-with-count js-toggler-target" aria-label="Unstar this repository" title="Unstar mapbox/help" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;UNSTAR_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;3EA2:92F6:11CA5C:1AB537:5D7026E4&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="94c94d5b76778251bd9ee9c3081cadbfed4f5a5c8fe553574ac2af205a0dec1f" data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">        <svg class="octicon octicon-star v-align-text-bottom" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74L14 6z"/></svg>
        Unstar
</button>        <a class="social-count js-social-count" href="/mapbox/help/stargazers"
           aria-label="3 users starred this repository">
           3
        </a>
</form>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="unstarred js-social-form" action="/mapbox/help/star" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="I6gv/Y6faWzl6/RAQr6YmFuN+J9mpjqpdoyTVZu6rfNCAZhEW4ser22IKsx2AqhOLRFFRzhB5gyVHCsKmKbxGA==" />
      <input type="hidden" name="context" value="repository"></input>
      <button type="submit" class="btn btn-sm btn-with-count js-toggler-target" aria-label="Unstar this repository" title="Star mapbox/help" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;STAR_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;3EA2:92F6:11CA5C:1AB537:5D7026E4&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="f48d47937d22212a77d32d29205134e986712e1f89a3532babdc61713b4b69ad" data-ga-click="Repository, click star button, action:blob#show; text:Star">        <svg class="octicon octicon-star v-align-text-bottom" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74L14 6z"/></svg>
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

    
    


  


    <a class="d-none js-permalink-shortcut" data-hotkey="y" href="/mapbox/help/blob/965b7620e7e1124ef6ac3d7b8dd90287324eae45/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md">Permalink</a>

    <!-- blob contrib key: blob_contributors:v21:41112574465892daf9d3760fcf6f9e12 -->
      

    <div class="d-flex flex-items-start flex-shrink-0 pb-3 flex-column flex-md-row">
      <span class="d-flex flex-justify-between width-full width-md-auto">
        
<details class="details-reset details-overlay select-menu branch-select-menu  hx_rsm" id="branch-select-menu">
  <summary class="btn btn-sm select-menu-button css-truncate"
           data-hotkey="w"
           title="publisher-production">
    <i>Branch:</i>
    <span class="css-truncate-target" data-menu-button>publisher-prod…</span>
  </summary>

  <details-menu class="select-menu-modal hx_rsm-modal position-absolute" style="z-index: 99;" src="/mapbox/help/ref-list/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md?source_action=show&amp;source_controller=blob" preload>
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
          <clipboard-copy value="src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md" class="btn btn-sm BtnGroup-item">
            Copy path
          </clipboard-copy>
        </div>
      </span>
      <h2 id="blob-path" class="breadcrumb flex-auto min-width-0 text-normal flex-md-self-center ml-md-2 mr-md-3 my-2 my-md-0">
        <span class="js-repo-root text-bold"><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help"><span>help</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src"><span>src</span></a></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src/pages"><span>pages</span></a></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src/pages/tutorials"><span>tutorials</span></a></span><span class="separator">/</span><strong class="final-path">make-a-heatmap-with-mapbox-gl-js.md</strong>
      </h2>

      <div class="BtnGroup flex-shrink-0 d-none d-md-inline-block">
        <a href="/mapbox/help/find/publisher-production"
              class="js-pjax-capture-input btn btn-sm BtnGroup-item"
              data-pjax
              data-hotkey="t">
          Find file
        </a>
        <clipboard-copy value="src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md" class="btn btn-sm BtnGroup-item">
          Copy path
        </clipboard-copy>
      </div>
    </div>



    <include-fragment src="/mapbox/help/contributors/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md" class="Box Box--condensed commit-loader">
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
      273 lines (230 sloc)
      <span class="file-info-divider"></span>
    14.3 KB
  </div>

  <div class="d-flex py-1 py-md-0 flex-auto flex-order-1 flex-md-order-2 flex-sm-grow-0 flex-justify-between">

    <div class="BtnGroup">
      <a id="raw-url" class="btn btn-sm BtnGroup-item" href="/mapbox/help/raw/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md">Raw</a>
        <a class="btn btn-sm js-update-url-with-hash BtnGroup-item" data-hotkey="b" href="/mapbox/help/blame/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md">Blame</a>
      <a rel="nofollow" class="btn btn-sm BtnGroup-item" href="/mapbox/help/commits/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md">History</a>
    </div>


    <div>
            <a class="btn-octicon tooltipped tooltipped-nw"
               href="x-github-client://openRepo/https://github.com/mapbox/help?branch=publisher-production&amp;filepath=src%2Fpages%2Ftutorials%2Fmake-a-heatmap-with-mapbox-gl-js.md"
               aria-label="Open this file in GitHub Desktop"
               data-ga-click="Repository, open with desktop, type:mac">
                <svg class="octicon octicon-device-desktop" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"/></svg>
            </a>

            <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="inline-form js-update-url-with-hash" action="/mapbox/help/edit/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="Nkct37hduHsQpqSVovm/SNpRgZo8IW1mvg1vVyVyhZLQlA2UlN1pEdOdm4hgs1F1+HnbXehDOw60mgau5N9aIQ==" />
              <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
                aria-label="Edit this file" data-hotkey="e" data-disable-with>
                <svg class="octicon octicon-pencil" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"/></svg>
              </button>
</form>
          <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="inline-form" action="/mapbox/help/delete/publisher-production/src/pages/tutorials/make-a-heatmap-with-mapbox-gl-js.md" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="n4yq7Kfc5r3Wo6R1RfdZaUVXUG//GiFvUTpE2Vkijhlex3Pqp33Ius9+Zm7PNRCHyXX9d3j8ChR+ybQkwcvtcw==" />
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
  <td><div>Make a heatmap with Mapbox GL JS</div></td>
  <td><div>Add custom HTML markers, style them, and add tooltips with Mapbox GL JS.</div></td>
  <td><div>makeAHeatmapWithMapboxGlJs</div></td>
  <td><div>2</div></td>
  <td><div><table>
  <tbody>
  <tr>
  <td><div>web apps</div></td>
  <td><div>map design</div></td>
  <td><div>data</div></td>
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
  <td><div>Familiarity with front-end development concepts.</div></td>
  <td><div><table>
  <tbody>
  <tr>
  <td><div>import * as constants from '../../constants';</div></td>
  <td><div>import Note from '@mapbox/dr-ui/note';</div></td>
  <td><div>import BookImage from '@mapbox/dr-ui/book-image';</div></td>
  <td><div>import Icon from '@mapbox/mr-ui/icon';</div></td>
  <td><div>import UserAccessToken from '../../components/user-access-token';</div></td>
  <td><div>import DemoIframe from '@mapbox/dr-ui/demo-iframe';</div></td>
  <td><div>import Button from '@mapbox/mr-ui/button';</div></td>
  </tr>
  </tbody>
</table>
</div></td>
  <td><div>tutorial</div></td>
  </tr>
  </tbody>
</table>

<p>In this guide, you will learn how to make a heatmap using <a href="https://www.mapbox.com/mapbox-gl-js/api/" rel="nofollow">Mapbox GL JS</a>. Heatmaps can be used to display large amounts of points in a way that is visually engaging and encourages your audience to explore your map.</p>
<p>{{

}}</p>
<h2><a id="user-content-getting-started" class="anchor" aria-hidden="true" href="#getting-started"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Getting started</h2>
<ul>
<li><strong>A Mapbox account and access token</strong>. Sign up for an account at mapbox.com/signup. You can find your access tokens on your <a href="https://www.mapbox.com/account" rel="nofollow">Account page</a>.</li>
<li><a href="https://www.mapbox.com/mapbox-gl-js" rel="nofollow"><strong>Mapbox GL JS</strong></a>. The Mapbox JavaScript API for building web maps.</li>
<li><strong>Data</strong>. In this tutorial, you’ll be using a GeoJSON file of street trees in the city of Pittsburgh from the <a href="http://www.wprdc.org/" rel="nofollow">Western Pennsylvania Regional Data Center</a>.</li>
</ul>
<p>{{
&lt;Button href="/help/demos/heatmap/trees.geojson" passthroughProps={{ download: "trees.geojson" }} &gt;
 Download GeoJSON

}}</p>
<h2><a id="user-content-what-is-the-purpose-of-a-heatmap" class="anchor" aria-hidden="true" href="#what-is-the-purpose-of-a-heatmap"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>What is the purpose of a heatmap?</h2>
<p>The term "heatmap" can refer to a few different kinds of cartographic visualizations. You may see it applied to presidential election maps, population density maps, or even meteorological maps.</p>
<p>Among maps you'll find on the web, there are two common categories of heatmaps: those that encourage the user to explore dense point data, and those that interpolate discrete values over a continuous surface, creating a smooth gradient between those points. The latter is less common and most often used in scientific publications or when a phenomenon is distributed over an area in a predictable way. For example, your town may only have a few weather stations, but your favorite weather app displays a smooth gradient of temperatures across the entire area of your town. For your local weather service, it is reasonable to assume that, if two adjacent stations report different temperatures, the temperature between them will transition gradually from one to the next.</p>
<p>For the purposes of this tutorial, we are referring to a different kind of visualization that is more useful for showing the <strong>density</strong> of points over an area. This type of heatmap does not visualize density by aggregating features within a set of boundaries in the way a <a href="/mapbox/help/blob/publisher-production/help/tutorials/choropleth-studio-gl-pt-1">choropleth</a> map does, but instead displays a continuous gradient between points.</p>
<p>Heatmaps aren't only useful for visualizing point density. They can also help visualize relative differences between those points. You can assign each point a higher or lower importance based on the value of a particular property within the dataset. In this tutorial, you will weight your map by the <code>DBH</code> property in your data. <code>DBH</code> stands for "diameter at breast height" and is a standard way of measuring a tree's diameter at 4.5 feet above the ground. In general, it is safe to assume that a tree with a higher <code>DBH</code> is older and larger. When you give these larger trees a higher weight compared to smaller saplings, your visualization can be an effective approximation of the area that is shaded by trees' leaves.</p>
<h2><a id="user-content-heatmap-paint-properties" class="anchor" aria-hidden="true" href="#heatmap-paint-properties"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Heatmap paint properties</h2>

<p>To add a <a href="https://www.mapbox.com/mapbox-gl-js/style-spec/#layers-heatmap" rel="nofollow">heatmap layer</a> to your map, you will need to configure a few properties. Understanding what these properties mean is key to creating a heatmap that accurately represents your data and strikes the right balance between too much detail and being a single, generalized blob.</p>
<ul>
<li><strong>heatmap-weight</strong>: Measures how much each individual point contributes to the appearace of your heatmap. Heatmap layers have a weight of one by default, which means that all points are weighted equally. Increasing the <code>heatmap-weight</code> property to five has the same effect as placing five points in the same location. You can use a stop function to set the weight of your points based on a specified property.</li>
<li><strong>heatmap-intensity</strong>: A multiplier on top of <code>heatmap-weight</code> that is primarily used as a convenient way to adjust the appearance of the heatmap based on zoom level.</li>
<li><strong>heatmap-color</strong>: Defines the heatmap's color gradient, from miniumum value to maximum value. The color displayed is dependent on the <a href="https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-heatmap-density" rel="nofollow">heatmap-density</a> value of each pixel (ranging from <code>0.0</code> to <code>1.0</code>). The value of this property is an <a href="https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions" rel="nofollow">expression</a> that uses heatmap-density as the input. For inspiration on color choices for your heatmap, take a look at <a href="http://colorbrewer2.org/#type=sequential&amp;scheme=BuGn&amp;n=3" rel="nofollow">Color Brewer</a>.</li>
<li><strong>heatmap-radius</strong>: Sets the radius for each point in pixels. The bigger the radius, the smoother the heatmap and the less amount of detail.</li>
<li><strong>heatmap-opacity</strong>: Controls the global opacity of the heatmap layer.</li>
</ul>
<h2><a id="user-content-create-your-map-using-mapbox-gl-js" class="anchor" aria-hidden="true" href="#create-your-map-using-mapbox-gl-js"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Create your map using Mapbox GL JS</h2>
<p>Now that you understand the purpose of heatmaps and the paint properties you will be working with, it's time to set up your map. For this example, you will be using the Mapbox Dark <a href="https://www.mapbox.com/studio-manual/reference/styles/#mapbox-template-styles" rel="nofollow">template style</a>. You can find the <a href="/mapbox/help/blob/publisher-production/help/glossary/style-url">Style URLs</a> for each of the template styles in <a href="https://docs.mapbox.com/api/maps/#styles" rel="nofollow">our API documentation</a>.</p>
<p>In your text editor, create a new <code>index.html</code> file, then copy and paste the below code into it. Make sure to replace <code>{{ &lt;UserAccessToken /&gt; }}</code> with an <a href="/mapbox/help/blob/publisher-production/help/glossary/access-token">access token</a> that is associated with your account. Once you add this code and save your <code>index.html</code> file, you can preview the file in your browser to make sure you see the map.</p>
<p>{{
&lt;Note imageComponent={}&gt;
</p><p>Be sure to save and store the GeoJSON file in the same directory as your project. You will also need to run this application from a local web server, otherwise you will receive a <a href="http://en.wikipedia.org/wiki/Cross-origin_resource_sharing" rel="nofollow">Cross-origin Resource Sharing (CORS)</a> error. <a href="http://www.2ality.com/2014/06/simple-http-server.html" rel="nofollow">Python's SimpleHTTPServer</a> is included on many computers and is a good choice if this is your first time running a local server.</p>

}}<p></p>
<div class="highlight highlight-text-html-basic"><pre>&lt;!DOCTYPE html&gt;
&lt;<span class="pl-ent">html</span>&gt;
&lt;<span class="pl-ent">head</span>&gt;
    &lt;<span class="pl-ent">meta</span> <span class="pl-e">charset</span>=<span class="pl-s"><span class="pl-pds">'</span>utf-8<span class="pl-pds">'</span></span> /&gt;
    &lt;<span class="pl-ent">title</span>&gt;&lt;/<span class="pl-ent">title</span>&gt;
    &lt;<span class="pl-ent">meta</span> <span class="pl-e">name</span>=<span class="pl-s"><span class="pl-pds">'</span>viewport<span class="pl-pds">'</span></span> <span class="pl-e">content</span>=<span class="pl-s"><span class="pl-pds">'</span>initial-scale=1,maximum-scale=1,user-scalable=no<span class="pl-pds">'</span></span> /&gt;
    &lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;
    &lt;<span class="pl-ent">link</span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css<span class="pl-pds">'</span></span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">'</span>stylesheet<span class="pl-pds">'</span></span> /&gt;
    &lt;<span class="pl-ent">style</span>&gt;<span class="pl-s1"></span>
<span class="pl-s1">      <span class="pl-ent">body</span> {</span>
<span class="pl-s1">        <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">        <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      }</span>
<span class="pl-s1"></span>
<span class="pl-s1">      <span class="pl-e">#map</span> {</span>
<span class="pl-s1">        <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;</span>
<span class="pl-s1">        <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">        <span class="pl-c1"><span class="pl-c1">bottom</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">        <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">100<span class="pl-k">%</span></span>;</span>
<span class="pl-s1">      }</span>
<span class="pl-s1">    </span>&lt;/<span class="pl-ent">style</span>&gt;
&lt;/<span class="pl-ent">head</span>&gt;
&lt;<span class="pl-ent">body</span>&gt;
  &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">div</span>&gt;
  &lt;<span class="pl-ent">script</span>&gt;<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>{{ &lt;UserAccessToken /&gt; }}<span class="pl-pds">'</span></span>;</span>
<span class="pl-s1">    <span class="pl-k">var</span> map <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">mapboxgl.Map</span>({</span>
<span class="pl-s1">      container<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span>,</span>
<span class="pl-s1">      style<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>mapbox://styles/mapbox/dark-v{{constants.VERSION_DARK_STYLE}}<span class="pl-pds">'</span></span>,</span>
<span class="pl-s1">      center<span class="pl-k">:</span> [<span class="pl-k">-</span><span class="pl-c1">79.999732</span>, <span class="pl-c1">40.4374</span>],</span>
<span class="pl-s1">      zoom<span class="pl-k">:</span> <span class="pl-c1">11</span></span>
<span class="pl-s1">    });</span>
<span class="pl-s1"></span>
<span class="pl-s1">   <span class="pl-c"><span class="pl-c">//</span> we will add more code here in the next steps</span></span>
<span class="pl-s1"></span>
<span class="pl-s1">  </span>&lt;/<span class="pl-ent">script</span>&gt;
&lt;/<span class="pl-ent">body</span>&gt;
&lt;/<span class="pl-ent">html</span>&gt;
</pre></div>
<h3><a id="user-content-add-your-data" class="anchor" aria-hidden="true" href="#add-your-data"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add your data</h3>
<p>You will first need to add the GeoJSON you downloaded at the beginning of this guide as the source for your heatmap. You can do this by using the <a href="https://www.mapbox.com/mapbox-gl-js/api/#map#addsource" rel="nofollow"><code>addSource</code></a> method. This source will be used to create not only a heatmap layer but also a circle layer. The heatmap layer will fade out while the circle layer fades in to show individual data points at higher zoom levels. Add the following code after the map you initialized in the previous step.</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>load<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>() {

  <span class="pl-smi">map</span>.<span class="pl-en">addSource</span>(<span class="pl-s"><span class="pl-pds">'</span>trees<span class="pl-pds">'</span></span>, {
    type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>geojson<span class="pl-pds">'</span></span>,
    data<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>./trees.geojson<span class="pl-pds">'</span></span>
  });
  <span class="pl-c"><span class="pl-c">//</span> add heatmap layer here</span>
  <span class="pl-c"><span class="pl-c">//</span> add circle layer here</span>
});</pre></div>
<h3><a id="user-content-add-the-heatmap-layer" class="anchor" aria-hidden="true" href="#add-the-heatmap-layer"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add the heatmap layer</h3>
<p>Next, use the <a href="https://www.mapbox.com/mapbox-gl-js/api/#map#addlayer" rel="nofollow"><code>addLayer</code></a> method to create a new layer for your heatmap. Once you've created this layer, you will make use of the heatmap properties discussed earlier to fine-tune your heatmap's appearance.</p>
<p>For <code>heatmap-weight</code>, specify a range that reflects your data (the <code>dbh</code> property ranges from 1-62 in the GeoJSON source). Because larger trees have a high <code>dbh</code>, give them more weight in your heatmap by creating a stop function that increases <code>heatmap-weight</code> as <code>dbh</code> increases.</p>
<p>Since <code>heatmap-intensity</code> is a multiplier on top of <code>heatmap-weight</code>, <code>heatmap-intensity</code> can be increased as the map zooms in to preserve a similar appearance throughout the zoom range. The images below show the impact of <code>heatmap-intensity</code> on your map's appearance. The image on the left shows <code>heatmap-intensity</code> that increases with zoom level and the one on the right shows <code>heatmap-intensity</code> that uses the default of <code>1</code>.</p>
<p>{{</p>
<div>
  <a target="_blank" rel="noopener noreferrer" href="/mapbox/help/blob/publisher-production/help/img/gl-js/heatmap-intensity-two.png"><img alt="demonstrates a heatmap-intensity that increases with zoom level" src="/mapbox/help/raw/publisher-production/help/img/gl-js/heatmap-intensity-two.png" style="max-width:100%;"></a>
  <a target="_blank" rel="noopener noreferrer" href="/mapbox/help/blob/publisher-production/help/img/gl-js/heatmap-intensity-one.png"><img alt="demonstrates heatmap intensity default of one" src="/mapbox/help/raw/publisher-production/help/img/gl-js/heatmap-intensity-one.png" style="max-width:100%;"></a>
</div>
}}
<p>For <code>heatmap-color</code>, add an <a href="https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-interpolate" rel="nofollow">interpolate</a> expression that defines a linear relationship between heatmap-density and heatmap-color using a set of input-output pairs. If you are interested in learning more about Mapbox GL JS Expressions, read the <a href="/mapbox/help/blob/publisher-production/help/tutorials/mapbox-gl-js-expressions">Get Started with Mapbox GL JS expressions guide</a> and the <a href="https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions" rel="nofollow">Mapbox GL JS documentation</a>.</p>
<p>Finish configuring your heatmap layer by setting values for <code>heatmap-radius</code> and <code>heatmap-opacity</code>. <code>heatmap-radius</code> should increase with zoom level to preserve the smoothness of the heatmap as the points become more dispersed. <code>heatmap-opacity</code> should be decreased from <code>1</code> to <code>0</code>  between zoom levels 14 and 15 to provide a smooth transition as your circle layer fades in to replace the heatmap layer. Add the following code within the 'load' event handler after the <code>addSource</code> method.</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">map</span>.<span class="pl-en">addLayer</span>({
  id<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>trees-heat<span class="pl-pds">'</span></span>,
  type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>heatmap<span class="pl-pds">'</span></span>,
  source<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>trees<span class="pl-pds">'</span></span>,
  maxzoom<span class="pl-k">:</span> <span class="pl-c1">15</span>,
  paint<span class="pl-k">:</span> {
    <span class="pl-c"><span class="pl-c">//</span> increase weight as diameter breast height increases</span>
    <span class="pl-s"><span class="pl-pds">'</span>heatmap-weight<span class="pl-pds">'</span></span><span class="pl-k">:</span> {
      property<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>dbh<span class="pl-pds">'</span></span>,
      type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>exponential<span class="pl-pds">'</span></span>,
      stops<span class="pl-k">:</span> [
        [<span class="pl-c1">1</span>, <span class="pl-c1">0</span>],
        [<span class="pl-c1">62</span>, <span class="pl-c1">1</span>]
      ]
    },
    <span class="pl-c"><span class="pl-c">//</span> increase intensity as zoom level increases</span>
    <span class="pl-s"><span class="pl-pds">'</span>heatmap-intensity<span class="pl-pds">'</span></span><span class="pl-k">:</span> {
      stops<span class="pl-k">:</span> [
        [<span class="pl-c1">11</span>, <span class="pl-c1">1</span>],
        [<span class="pl-c1">15</span>, <span class="pl-c1">3</span>]
      ]
    },
    <span class="pl-c"><span class="pl-c">//</span> assign color values be applied to points depending on their density</span>
    <span class="pl-s"><span class="pl-pds">'</span>heatmap-color<span class="pl-pds">'</span></span><span class="pl-k">:</span> [
      <span class="pl-s"><span class="pl-pds">'</span>interpolate<span class="pl-pds">'</span></span>,
      [<span class="pl-s"><span class="pl-pds">'</span>linear<span class="pl-pds">'</span></span>],
      [<span class="pl-s"><span class="pl-pds">'</span>heatmap-density<span class="pl-pds">'</span></span>],
      <span class="pl-c1">0</span>, <span class="pl-s"><span class="pl-pds">'</span>rgba(236,222,239,0)<span class="pl-pds">'</span></span>,
      <span class="pl-c1">0.2</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(208,209,230)<span class="pl-pds">'</span></span>,
      <span class="pl-c1">0.4</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(166,189,219)<span class="pl-pds">'</span></span>,
      <span class="pl-c1">0.6</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(103,169,207)<span class="pl-pds">'</span></span>,
      <span class="pl-c1">0.8</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(28,144,153)<span class="pl-pds">'</span></span>
    ],
    <span class="pl-c"><span class="pl-c">//</span> increase radius as zoom increases</span>
    <span class="pl-s"><span class="pl-pds">'</span>heatmap-radius<span class="pl-pds">'</span></span><span class="pl-k">:</span> {
      stops<span class="pl-k">:</span> [
        [<span class="pl-c1">11</span>, <span class="pl-c1">15</span>],
        [<span class="pl-c1">15</span>, <span class="pl-c1">20</span>]
      ]
    },
    <span class="pl-c"><span class="pl-c">//</span> decrease opacity to transition into the circle layer</span>
    <span class="pl-s"><span class="pl-pds">'</span>heatmap-opacity<span class="pl-pds">'</span></span><span class="pl-k">:</span> {
      default<span class="pl-k">:</span> <span class="pl-c1">1</span>,
      stops<span class="pl-k">:</span> [
        [<span class="pl-c1">14</span>, <span class="pl-c1">1</span>],
        [<span class="pl-c1">15</span>, <span class="pl-c1">0</span>]
      ]
    },
  }
}, <span class="pl-s"><span class="pl-pds">'</span>waterway-label<span class="pl-pds">'</span></span>);</pre></div>
<h3><a id="user-content-add-the-circle-layer" class="anchor" aria-hidden="true" href="#add-the-circle-layer"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add the circle layer</h3>
<p>Next, add a circle layer. As you zoom in to your heatmap, the points stop overlapping visually and it is no longer necessary to show their distribution and density. At this point, you can show the points themselves and allow viewers to explore the data interactively.</p>
<p>Remember how you used a stop function in the previous step to fade the heatmap layer out between zoom level 14 and 15? You'll need to replace that layer by fading your circle layer in, using a zoom function to increase its <code>circle-opacity</code> between zooms 14 and 15. For <code>circle-radius</code>, use a zoom-and-property function to increase the radius by zoom level and property (as demonstrated below). Add the following code after the heatmap layer you added in the last step.</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">map</span>.<span class="pl-en">addLayer</span>({
  id<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>trees-point<span class="pl-pds">'</span></span>,
  type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>circle<span class="pl-pds">'</span></span>,
  source<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>trees<span class="pl-pds">'</span></span>,
  minzoom<span class="pl-k">:</span> <span class="pl-c1">14</span>,
  paint<span class="pl-k">:</span> {
    <span class="pl-c"><span class="pl-c">//</span> increase the radius of the circle as the zoom level and dbh value increases</span>
    <span class="pl-s"><span class="pl-pds">'</span>circle-radius<span class="pl-pds">'</span></span><span class="pl-k">:</span> {
      property<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>dbh<span class="pl-pds">'</span></span>,
      type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>exponential<span class="pl-pds">'</span></span>,
      stops<span class="pl-k">:</span> [
        [{ zoom<span class="pl-k">:</span> <span class="pl-c1">15</span>, value<span class="pl-k">:</span> <span class="pl-c1">1</span> }, <span class="pl-c1">5</span>],
        [{ zoom<span class="pl-k">:</span> <span class="pl-c1">15</span>, value<span class="pl-k">:</span> <span class="pl-c1">62</span> }, <span class="pl-c1">10</span>],
        [{ zoom<span class="pl-k">:</span> <span class="pl-c1">22</span>, value<span class="pl-k">:</span> <span class="pl-c1">1</span> }, <span class="pl-c1">20</span>],
        [{ zoom<span class="pl-k">:</span> <span class="pl-c1">22</span>, value<span class="pl-k">:</span> <span class="pl-c1">62</span> }, <span class="pl-c1">50</span>],
      ]
    },
    <span class="pl-s"><span class="pl-pds">'</span>circle-color<span class="pl-pds">'</span></span><span class="pl-k">:</span> {
      property<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>dbh<span class="pl-pds">'</span></span>,
      type<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>exponential<span class="pl-pds">'</span></span>,
      stops<span class="pl-k">:</span> [
        [<span class="pl-c1">0</span>, <span class="pl-s"><span class="pl-pds">'</span>rgba(236,222,239,0)<span class="pl-pds">'</span></span>],
        [<span class="pl-c1">10</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(236,222,239)<span class="pl-pds">'</span></span>],
        [<span class="pl-c1">20</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(208,209,230)<span class="pl-pds">'</span></span>],
        [<span class="pl-c1">30</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(166,189,219)<span class="pl-pds">'</span></span>],
        [<span class="pl-c1">40</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(103,169,207)<span class="pl-pds">'</span></span>],
        [<span class="pl-c1">50</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(28,144,153)<span class="pl-pds">'</span></span>],
        [<span class="pl-c1">60</span>, <span class="pl-s"><span class="pl-pds">'</span>rgb(1,108,89)<span class="pl-pds">'</span></span>]
      ]
    },
    <span class="pl-s"><span class="pl-pds">'</span>circle-stroke-color<span class="pl-pds">'</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>white<span class="pl-pds">'</span></span>,
    <span class="pl-s"><span class="pl-pds">'</span>circle-stroke-width<span class="pl-pds">'</span></span><span class="pl-k">:</span> <span class="pl-c1">1</span>,
    <span class="pl-s"><span class="pl-pds">'</span>circle-opacity<span class="pl-pds">'</span></span><span class="pl-k">:</span> {
      stops<span class="pl-k">:</span> [
        [<span class="pl-c1">14</span>, <span class="pl-c1">0</span>],
        [<span class="pl-c1">15</span>, <span class="pl-c1">1</span>]
      ]
    }
  }
}, <span class="pl-s"><span class="pl-pds">'</span>waterway-label<span class="pl-pds">'</span></span>);</pre></div>
<h2><a id="user-content-add-some-additional-interactivity" class="anchor" aria-hidden="true" href="#add-some-additional-interactivity"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add some additional interactivity</h2>
<p>The following code adds interactivity to your map by allowing your viewers to click on your circle layer to view a popup containing the tree's <code>DBH</code> value. Include the code below after your circle layer.</p>
<p>{{<a target="_blank" rel="noopener noreferrer" href="/mapbox/help/blob/publisher-production/help/img/gl-js/heatmap-popup.gif"><img src="/mapbox/help/raw/publisher-production/help/img/gl-js/heatmap-popup.gif" alt="demonstrates how to add a popup to the circle layer of a heatmap" style="max-width:100%;"></a>}}</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>click<span class="pl-pds">'</span></span>, <span class="pl-s"><span class="pl-pds">'</span>trees-point<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>(<span class="pl-smi">e</span>) {
  <span class="pl-k">new</span> <span class="pl-en">mapboxgl.Popup</span>()
    .<span class="pl-en">setLngLat</span>(<span class="pl-smi">e</span>.<span class="pl-smi">features</span>[<span class="pl-c1">0</span>].<span class="pl-smi">geometry</span>.<span class="pl-smi">coordinates</span>)
    .<span class="pl-en">setHTML</span>(<span class="pl-s"><span class="pl-pds">'</span>&lt;b&gt;DBH:&lt;/b&gt; <span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-smi">e</span>.<span class="pl-smi">features</span>[<span class="pl-c1">0</span>].<span class="pl-smi">properties</span>.<span class="pl-smi">dbh</span>)
    .<span class="pl-en">addTo</span>(map);
});
</pre></div>
<h2><a id="user-content-finished-product" class="anchor" aria-hidden="true" href="#finished-product"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Finished product</h2>
<p>Congrats! You made your first heatmap with Mapbox GL JS!</p>
<p>{{

}}</p>
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
      <li class="mr-3 mr-lg-0">&copy; 2019 <span title="0.44234s from unicorn-59585b5b69-dkj2n">GitHub</span>, Inc.</li>
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

