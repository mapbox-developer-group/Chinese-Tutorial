





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
  
  <title>help/get-started-map-matching-api.md at publisher-production · mapbox/help</title>
    <meta name="description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub.">
    <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
  <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
  <meta property="fb:app_id" content="1401488693436528">

    <meta name="twitter:image:src" content="https://avatars2.githubusercontent.com/u/600935?s=400&amp;v=4" /><meta name="twitter:site" content="@github" /><meta name="twitter:card" content="summary" /><meta name="twitter:title" content="mapbox/help" /><meta name="twitter:description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub." />
    <meta property="og:image" content="https://avatars2.githubusercontent.com/u/600935?s=400&amp;v=4" /><meta property="og:site_name" content="GitHub" /><meta property="og:type" content="object" /><meta property="og:title" content="mapbox/help" /><meta property="og:url" content="https://github.com/mapbox/help" /><meta property="og:description" content="Mapbox help doc &amp; guides. Contribute to mapbox/help development by creating an account on GitHub." />

  <link rel="assets" href="https://github.githubassets.com/">
  <link rel="web-socket" href="wss://live.github.com/_sockets/VjI6MzAyOTU4NTE3OmNjZWRmOTM5NWUxNWI4YTg1ODY5ZDZmNDhjYmYzYzRmMzI3OTczYzgyNDk0Y2M1YjU4MGZjNzJhZTc0MjJhYzQ=--aa3945910f1af8a6f8aaca2c28de8ec00c26f6ae">
  <meta name="pjax-timeout" content="1000">
  <link rel="sudo-modal" href="/sessions/sudo_modal">
  <meta name="request-id" content="38F0:9477:10DBA2:197B0E:5D7025DD" data-pjax-transient>


  <link rel="sso-modal" href="/orgs/mapbox/sso_modal" data-pjax-transient="true"></link><link rel="sso-session" href="/orgs/mapbox/sso_status.json" data-pjax-transient="true"></link><meta name="sso-expires-around" content="1567704602" data-pjax-transient="true"></meta>

  <meta name="selected-link" value="repo_source" data-pjax-transient>

      <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
    <meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-site-verification" content="GXs5KoUUkNCoaAZn7wPN-t01Pywp9M3sEjnt_3_ZWPc">

  <meta name="octolytics-host" content="collector.githubapp.com" /><meta name="octolytics-app-id" content="github" /><meta name="octolytics-event-url" content="https://collector.githubapp.com/github-external/browser_event" /><meta name="octolytics-dimension-request_id" content="38F0:9477:10DBA2:197B0E:5D7025DD" /><meta name="octolytics-dimension-region_edge" content="sea" /><meta name="octolytics-dimension-region_render" content="iad" /><meta name="octolytics-dimension-ga_id" content="" class="js-octo-ga-id" /><meta name="octolytics-dimension-visitor_id" content="2058165157458336909" /><meta name="octolytics-actor-id" content="18397640" /><meta name="octolytics-actor-login" content="Jing-flyloveyin" /><meta name="octolytics-actor-hash" content="c7be0e1b8bc813e56ceee222f4a1c9e2890774570591d5891573b62c21660107" />
<meta name="analytics-location" content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" />



    <meta name="google-analytics" content="UA-3769691-2">

  <meta class="js-ga-set" name="userId" content="a377d279e504cd9111bf6c4e502c8d97">

<meta class="js-ga-set" name="dimension1" content="Logged In">



  

      <meta name="hostname" content="github.com">
    <meta name="user-login" content="Jing-flyloveyin">

      <meta name="expected-hostname" content="github.com">
    <meta name="js-proxy-site-detection-payload" content="NDc3NTYwMWEzMDAxMjM0MDcyM2JjMWEzYTRmODZmYmE4NWY1NWQ2OWVjMTFlNTA0ODJiZTI2NDgzZjUyNjVmY3x7InJlbW90ZV9hZGRyZXNzIjoiNDUuNzkuODMuODEiLCJyZXF1ZXN0X2lkIjoiMzhGMDo5NDc3OjEwREJBMjoxOTdCMEU6NUQ3MDI1REQiLCJ0aW1lc3RhbXAiOjE1Njc2MzA4MjcsImhvc3QiOiJnaXRodWIuY29tIn0=">

    <meta name="enabled-features" content="ACTIONS_V2_ON_MARKETPLACE,MARKETPLACE_FEATURED_BLOG_POSTS,MARKETPLACE_INVOICED_BILLING,MARKETPLACE_SOCIAL_PROOF_CUSTOMERS,MARKETPLACE_TRENDING_SOCIAL_PROOF,MARKETPLACE_RECOMMENDATIONS,MARKETPLACE_PENDING_INSTALLATIONS,NOTIFY_ON_BLOCK,RELATED_ISSUES,GHE_CLOUD_TRIAL">

  <meta name="html-safe-nonce" content="fb97dd135de80342fdc477688b418fc612fd0e7e">

  <meta http-equiv="x-pjax-version" content="785dc78f1f1353014e3eece9d3f39215">
  

      <link href="https://github.com/mapbox/help/commits/publisher-production.atom?token=AEMLTSE4245EHSXKTC4HQXN3PVTHU" rel="alternate" title="Recent Commits to help:publisher-production" type="application/atom+xml">

  <meta name="go-import" content="github.com/mapbox/help git https://github.com/mapbox/help.git">

  <meta name="octolytics-dimension-user_id" content="600935" /><meta name="octolytics-dimension-user_login" content="mapbox" /><meta name="octolytics-dimension-repository_id" content="34758294" /><meta name="octolytics-dimension-repository_nwo" content="mapbox/help" /><meta name="octolytics-dimension-repository_public" content="false" /><meta name="octolytics-dimension-repository_is_fork" content="false" /><meta name="octolytics-dimension-repository_network_root_id" content="34758294" /><meta name="octolytics-dimension-repository_network_root_nwo" content="mapbox/help" /><meta name="octolytics-dimension-repository_explore_github_marketplace_ci_cta_shown" content="false" />


    <link rel="canonical" href="https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/get-started-map-matching-api.md" data-pjax-transient>


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
          data-jump-to-suggestions-path="/_graphql/GetSuggestedNavigationDestinations#csrf-token=dtjgePssEIodpEafHkrLIJs0QRH6H+nqmj/hvtm44Dz3cT0Yo8UjUW2BfOx4af0QxVZndoYEjqLWzLtO8NdOGg=="
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
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form action="/logout" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="Ob/DuQLv87AFDjkQpSGsFPWY+wah4pSOAsMFPgJFe0h9bfqCEBulB6fV0nTPUUCamuOX8gIMgU384Gg9GB936A==" />
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
      role="menuitem" data-hydro-click="{&quot;event_type&quot;:&quot;user_profile.click&quot;,&quot;payload&quot;:{&quot;profile_user_id&quot;:600935,&quot;target&quot;:&quot;EDIT_USER_STATUS&quot;,&quot;user_id&quot;:18397640,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;38F0:9477:10DBA2:197B0E:5D7025DD&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/get-started-map-matching-api.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;}}" data-hydro-click-hmac="d653ea567c6c237e86d7e79a84ca057de5a932596dfc9df90d4b6e503e65126e">
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
      <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="position-relative flex-auto js-user-status-form" action="/users/status?compact=1&amp;link_mentions=0&amp;truncate=1" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="_method" value="put" /><input type="hidden" name="authenticity_token" value="EZBFAaBoBdam4itCKocky88NCE75xOCSiDAERqh9XvdGbdnvacyK6WMm3kRpeU1isHVHOz6/nrqhvG+SEI/F5g==" />
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
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 30 minutes" value="2019-09-04T14:30:27-07:00">
            in 30 minutes
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 1 hour" value="2019-09-04T15:00:27-07:00">
            in 1 hour
          </button>
        </li>
        <li>
          <button type="button" class="btn-link dropdown-item ws-normal js-user-status-expire-button" title="in 4 hours" value="2019-09-04T18:00:27-07:00">
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
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="logout-form" action="/logout" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="jl3ZqX7WECKGEimcEzvw67EUj8EvWcfi5yAOKqTn1NfKj+CSbCJGlSTJwvh5Sxxl3m/jNYy30iEZA2Mpvr3Ydw==" />
      
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
      <a class="btn btn-primary shelf-cta" target="_blank" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;READ_GUIDE&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;38F0:9477:10DBA2:197B0E:5D7025DD&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/get-started-map-matching-api.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="f78cfce3ae4af97c94be7a82ca78bae65362dc6874bdf9b986a70152ff7fd53a" href="https://guides.github.com/activities/hello-world/">Read the guide</a>
    </div>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="shelf-dismiss js-notice-dismiss" action="/dashboard/dismiss_bootcamp" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="_method" value="delete" /><input type="hidden" name="authenticity_token" value="Em5Da3oL+MX3tTBmS3CfKfGX7lmHtn/4f1llLOtFvpsuzKVy8p7/OyuzACkUnjkXWbcd5Xl2Xzxv+YPRw9niLw==" />
      <button name="button" type="submit" class="mr-1 close-button tooltipped tooltipped-w" aria-label="Hide this notice forever" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;DISMISS_BANNER&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;38F0:9477:10DBA2:197B0E:5D7025DD&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/get-started-map-matching-api.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="7ee7dec231fd950540dada6412ed14d11ee843957cd412be999d87f3815a89a2">
        <svg aria-label="Hide this notice forever" class="octicon octicon-x v-align-text-top" viewBox="0 0 12 16" version="1.1" width="12" height="16" role="img"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48L7.48 8z"/></svg>
</button></form>  </div>
</div>



  








  <div class="pagehead repohead instapaper_ignore readability-menu experiment-repo-nav pt-0 pt-lg-4 ">
    <div class="repohead-details-container clearfix container-lg p-responsive d-none d-lg-block">

      <ul class="pagehead-actions">




  <li>
    
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form data-remote="true" class="clearfix js-social-form js-social-container" action="/notifications/subscribe" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="1T2iYLoRnhLW0XTc1ZxK8VSeWv3ri8nnQGYZBm3VI7x5Rn1y5dEJ8OuZ2BTLi7poABHPniUDozG+j5qEOVTEzA==" />      <input type="hidden" name="repository_id" value="34758294">

      <details class="details-reset details-overlay select-menu float-left">
        <summary class="select-menu-button float-left btn btn-sm btn-with-count" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;WATCH_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;38F0:9477:10DBA2:197B0E:5D7025DD&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/get-started-map-matching-api.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="2afff012fa02077b165f9c33576ddaf0ebe5173e6daa1b1a6141c2b8e0a9f5e9" data-ga-click="Repository, click Watch settings, action:blob#show">          <span data-menu-button>
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
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="starred js-social-form" action="/mapbox/help/unstar" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="mZlKBzXOp8gfqmW+Z5XbC7aQTNsEKBRboVGT+1DQwDD+H6wu/XZMmU8Ri8VLDD2p+tQRfTPL0juQHCDmtxyPKw==" />
      <input type="hidden" name="context" value="repository"></input>
      <button type="submit" class="btn btn-sm btn-with-count js-toggler-target" aria-label="Unstar this repository" title="Unstar mapbox/help" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;UNSTAR_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;38F0:9477:10DBA2:197B0E:5D7025DD&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/get-started-map-matching-api.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="03fc12b7fda38c5b5f84e57b7d550c66e590f6db39b2fe00e00404be7c7fb4b6" data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">        <svg class="octicon octicon-star v-align-text-bottom" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74L14 6z"/></svg>
        Unstar
</button>        <a class="social-count js-social-count" href="/mapbox/help/stargazers"
           aria-label="3 users starred this repository">
           3
        </a>
</form>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="unstarred js-social-form" action="/mapbox/help/star" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="br0GmZW3SPoFnbX4jW3Q2md/48Afi2ctbC5eoyC/y7YPFLEgQKM/OY3+a3S50eAMEeNeGEFsu4iPvub8I6OXXQ==" />
      <input type="hidden" name="context" value="repository"></input>
      <button type="submit" class="btn btn-sm btn-with-count js-toggler-target" aria-label="Unstar this repository" title="Star mapbox/help" data-hydro-click="{&quot;event_type&quot;:&quot;repository.click&quot;,&quot;payload&quot;:{&quot;target&quot;:&quot;STAR_BUTTON&quot;,&quot;repository_id&quot;:34758294,&quot;client_id&quot;:&quot;479203918.1533271181&quot;,&quot;originating_request_id&quot;:&quot;38F0:9477:10DBA2:197B0E:5D7025DD&quot;,&quot;originating_url&quot;:&quot;https://github.com/mapbox/help/blob/publisher-production/src/pages/tutorials/get-started-map-matching-api.md&quot;,&quot;referrer&quot;:&quot;https://github.com/mapbox/help/tree/publisher-production/src/pages/tutorials&quot;,&quot;user_id&quot;:18397640}}" data-hydro-click-hmac="82870b2cc626910881cdafbe34b60674ec87e89a04a0e586626de363a2bcccd1" data-ga-click="Repository, click star button, action:blob#show; text:Star">        <svg class="octicon octicon-star v-align-text-bottom" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74L14 6z"/></svg>
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

    
    


  


    <a class="d-none js-permalink-shortcut" data-hotkey="y" href="/mapbox/help/blob/965b7620e7e1124ef6ac3d7b8dd90287324eae45/src/pages/tutorials/get-started-map-matching-api.md">Permalink</a>

    <!-- blob contrib key: blob_contributors:v21:49ff05c512f5132c2b7b5971c4669640 -->
      

    <div class="d-flex flex-items-start flex-shrink-0 pb-3 flex-column flex-md-row">
      <span class="d-flex flex-justify-between width-full width-md-auto">
        
<details class="details-reset details-overlay select-menu branch-select-menu  hx_rsm" id="branch-select-menu">
  <summary class="btn btn-sm select-menu-button css-truncate"
           data-hotkey="w"
           title="publisher-production">
    <i>Branch:</i>
    <span class="css-truncate-target" data-menu-button>publisher-prod…</span>
  </summary>

  <details-menu class="select-menu-modal hx_rsm-modal position-absolute" style="z-index: 99;" src="/mapbox/help/ref-list/publisher-production/src/pages/tutorials/get-started-map-matching-api.md?source_action=show&amp;source_controller=blob" preload>
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
          <clipboard-copy value="src/pages/tutorials/get-started-map-matching-api.md" class="btn btn-sm BtnGroup-item">
            Copy path
          </clipboard-copy>
        </div>
      </span>
      <h2 id="blob-path" class="breadcrumb flex-auto min-width-0 text-normal flex-md-self-center ml-md-2 mr-md-3 my-2 my-md-0">
        <span class="js-repo-root text-bold"><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help"><span>help</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src"><span>src</span></a></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src/pages"><span>pages</span></a></span><span class="separator">/</span><span class="js-path-segment"><a data-pjax="true" href="/mapbox/help/tree/publisher-production/src/pages/tutorials"><span>tutorials</span></a></span><span class="separator">/</span><strong class="final-path">get-started-map-matching-api.md</strong>
      </h2>

      <div class="BtnGroup flex-shrink-0 d-none d-md-inline-block">
        <a href="/mapbox/help/find/publisher-production"
              class="js-pjax-capture-input btn btn-sm BtnGroup-item"
              data-pjax
              data-hotkey="t">
          Find file
        </a>
        <clipboard-copy value="src/pages/tutorials/get-started-map-matching-api.md" class="btn btn-sm BtnGroup-item">
          Copy path
        </clipboard-copy>
      </div>
    </div>



    <include-fragment src="/mapbox/help/contributors/publisher-production/src/pages/tutorials/get-started-map-matching-api.md" class="Box Box--condensed commit-loader">
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
      701 lines (596 sloc)
      <span class="file-info-divider"></span>
    29.3 KB
  </div>

  <div class="d-flex py-1 py-md-0 flex-auto flex-order-1 flex-md-order-2 flex-sm-grow-0 flex-justify-between">

    <div class="BtnGroup">
      <a id="raw-url" class="btn btn-sm BtnGroup-item" href="/mapbox/help/raw/publisher-production/src/pages/tutorials/get-started-map-matching-api.md">Raw</a>
        <a class="btn btn-sm js-update-url-with-hash BtnGroup-item" data-hotkey="b" href="/mapbox/help/blame/publisher-production/src/pages/tutorials/get-started-map-matching-api.md">Blame</a>
      <a rel="nofollow" class="btn btn-sm BtnGroup-item" href="/mapbox/help/commits/publisher-production/src/pages/tutorials/get-started-map-matching-api.md">History</a>
    </div>


    <div>
            <a class="btn-octicon tooltipped tooltipped-nw"
               href="x-github-client://openRepo/https://github.com/mapbox/help?branch=publisher-production&amp;filepath=src%2Fpages%2Ftutorials%2Fget-started-map-matching-api.md"
               aria-label="Open this file in GitHub Desktop"
               data-ga-click="Repository, open with desktop, type:mac">
                <svg class="octicon octicon-device-desktop" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"/></svg>
            </a>

            <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="inline-form js-update-url-with-hash" action="/mapbox/help/edit/publisher-production/src/pages/tutorials/get-started-map-matching-api.md" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="MdvY0PhQRpz7TtFw7YuH1afk1DM7Q4lH8+Dk1naKkmQ9zvIijHOHoUOUqyse/0N5wSuCkdGYkjNWjQ8wgCMt3A==" />
              <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
                aria-label="Edit this file" data-hotkey="e" data-disable-with>
                <svg class="octicon octicon-pencil" viewBox="0 0 14 16" version="1.1" width="14" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"/></svg>
              </button>
</form>
          <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="inline-form" action="/mapbox/help/delete/publisher-production/src/pages/tutorials/get-started-map-matching-api.md" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="fpDPxTEgfYf2S03bsfKBnIqLFI2kITQoeSFGG0OigbrUG7n83ETW7/AL/FRK2tPxU5xsQz5mh3sPwBTqD4ofaA==" />
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
  <th>topics</th>
  <th>level</th>
  <th>language</th>
  <th>prereq</th>
  <th>prependJs</th>
  <th>contentType</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div>Get started with the Map Matching API</div></td>
  <td><div>Create a web app that uses the Mapbox Map Matching API to allow users to specify their own driving route.</div></td>
  <td><div>mapMatchingGetStartedDirections</div></td>
  <td><div><table>
  <tbody>
  <tr>
  <td><div>navigation</div></td>
  <td><div>directions</div></td>
  <td><div>web apps</div></td>
  </tr>
  </tbody>
</table>
</div></td>
  <td><div>2</div></td>
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
  <td><div>import Note from '@mapbox/dr-ui/note';</div></td>
  <td><div>import BookImage from '@mapbox/dr-ui/book-image';</div></td>
  <td><div>import Icon from '@mapbox/mr-ui/icon';</div></td>
  <td><div>import DemoIframe from '@mapbox/dr-ui/demo-iframe';</div></td>
  <td><div>import UserAccessToken from '../../components/user-access-token';</div></td>
  <td><div>import * as constants from '../../constants';</div></td>
  <td><div>import AppropriateImage from '../../components/appropriate-image';</div></td>
  <td><div>import { ColorSwatch } from '../../components/color-swatch';</div></td>
  </tr>
  </tbody>
</table>
</div></td>
  <td><div>tutorial</div></td>
  </tr>
  </tbody>
</table>

<p>Most turn-by-turn apps assume that users want to take the most efficient route to their destination. But sometimes, users care more about being able to choose a fun or scenic route than they do about getting to their destination quickly. For example: <em>Your user is visiting San Francisco. They visited the Maritime Museum, and now it’s time to get a slice of pizza in North Beach. On the way, they want to drive down Lombard Street, a stretch of road with eight tight hairpin turns that’s popularly known as the “crookedest street in the world”.</em></p>
<p>Taking Lombard Street isn't the fastest way to get to the user’s destination, but it does offer more photo opportunities than any other route! In most turn-by-turn apps, it’s difficult to pull up a route that includes this stretch of Lombard Street because it’s not the most efficient route. This means a user would be routed elsewhere, regardless of their wish to drive down Lombard Street. But the <a href="https://docs.mapbox.com/api/navigation/#map-matching" rel="nofollow">Mapbox Map Matching API</a> makes it possible to plot custom routes, which opens up different routing possibilities.</p>
<p>In this tutorial, you will create a web application that allows your users to create their own travel routes, regardless of whether those routes are the most efficient routes or not. The app's users will draw their own route on the map using draw tools from the <strong>Mapbox GL Draw plugin</strong>, then the app will pass the drawn coordinates to the <strong>Map Matching API</strong> and generate turn-by-turn directions for the new driving route.</p>
<p>{{

}}</p>
<p>{{&lt;Note title="The Map Matching API vs. the Directions API" imageComponent={}&gt;}}</p>
<p>The Mapbox Map Matching API has a lot of similarities to the <a href="https://docs.mapbox.com/api/navigation/#directions" rel="nofollow">Directions API</a>. The Map Matching API can be used to generate routes, route durations, and turn-by-turn directions, as the Directions API can. But the Directions API will specifically always generate an <em>optimal</em> route, while the Map Matching API will generate a route on the OpenStreetMap road network that most closely follows the coordinates provided in the request.</p>
<p>{{}}</p>
<h2><a id="user-content-getting-started" class="anchor" aria-hidden="true" href="#getting-started"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Getting started</h2>
<p>To complete this tutorial, you will need:</p>
<ul>
<li><strong>A Mapbox access token.</strong> Your Mapbox access tokens are on your <a href="https://account.mapbox.com/" rel="nofollow">Account page</a>.</li>
<li><strong>Mapbox GL JS.</strong> <a href="https://docs.mapbox.com/mapbox-gl-js/overview/" rel="nofollow">Mapbox GL JS</a> is a JavaScript API for building web maps.</li>
<li><strong>Mapbox GL Draw plugin.</strong> The <a href="https://github.com/mapbox/mapbox-gl-draw">Mapbox GL Draw plugin</a> adds support for drawing and editing features on maps created with Mapbox GL JS.</li>
<li><strong>Mapbox Map Matching API.</strong> The <a href="https://docs.mapbox.com/api/navigation/#map-matching" rel="nofollow">Map Matching API</a> snaps coordinates onto the OpenStreetMap road network, and can return turn-by-turn directions for the routes it produces.</li>
<li><strong>jQuery.</strong> <a href="https://jquery.com/" rel="nofollow">jQuery</a> is a JavaScript library you will use to add your API request to your application.</li>
<li><strong>A text editor.</strong> Use the text editor of your choice for writing HTML, CSS, and JavaScript.</li>
</ul>
<h2><a id="user-content-create-a-map" class="anchor" aria-hidden="true" href="#create-a-map"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Create a map</h2>
<p>To start the app, you will create a map using <a href="https://docs.mapbox.com/mapbox-gl-js/api/" rel="nofollow">Mapbox GL JS</a>.</p>
<p>Open your text editor and create a new file named <code>index.html</code>. Set up this new HTML file by pasting the following code into your text editor. This code creates the structure of the page. This code also imports Mapbox GL JS and jQuery in the <code>&lt;head&gt;</code> of the page. The Mapbox GL JS JavaScript and CSS files allow you to use Mapbox GL JS functionality and style, while jQuery will allow you to use <a href="https://api.jquery.com/jquery.ajax/" rel="nofollow">Ajax</a> to parse your Map Matching API call.</p>
<p>There is a <code>&lt;div&gt;</code> element with the ID <code>map</code> in the <code>&lt;body&gt;</code> of the page. This <code>&lt;div&gt;</code> is the container in which the map will be displayed on the page.</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;!DOCTYPE html&gt;
&lt;<span class="pl-ent">html</span>&gt;

&lt;<span class="pl-ent">head</span>&gt;
  &lt;<span class="pl-ent">meta</span> <span class="pl-e">charset</span>=<span class="pl-s"><span class="pl-pds">'</span>utf-8<span class="pl-pds">'</span></span> /&gt;
  &lt;<span class="pl-ent">title</span>&gt;Get started with the Map Matching API&lt;/<span class="pl-ent">title</span>&gt;
  &lt;<span class="pl-ent">meta</span> <span class="pl-e">name</span>=<span class="pl-s"><span class="pl-pds">'</span>viewport<span class="pl-pds">'</span></span> <span class="pl-e">content</span>=<span class="pl-s"><span class="pl-pds">'</span>initial-scale=1,maximum-scale=1,user-scalable=no<span class="pl-pds">'</span></span> /&gt;
  <span class="pl-c"><span class="pl-c">&lt;!--</span> Import Mapbox GL JS  <span class="pl-c">--&gt;</span></span>
  &lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;
  &lt;<span class="pl-ent">link</span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css<span class="pl-pds">'</span></span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">'</span>stylesheet<span class="pl-pds">'</span></span> /&gt;
  <span class="pl-c"><span class="pl-c">&lt;!--</span> Import jQuery <span class="pl-c">--&gt;</span></span>
  &lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;

  &lt;<span class="pl-ent">style</span>&gt;<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-ent">body</span> {</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-e">#map</span> {</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">bottom</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">100<span class="pl-k">%</span></span>;</span>
<span class="pl-s1">    }</span>
<span class="pl-s1">  </span>&lt;/<span class="pl-ent">style</span>&gt;
&lt;/<span class="pl-ent">head</span>&gt;

&lt;<span class="pl-ent">body</span>&gt;
  <span class="pl-c"><span class="pl-c">&lt;!--</span> Create a container for the map <span class="pl-c">--&gt;</span></span>
  &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">div</span>&gt;

  &lt;<span class="pl-ent">script</span>&gt;<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-c"><span class="pl-c">//</span> Add your Mapbox access token</span></span>
<span class="pl-s1">    <span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>{{ &lt;UserAccessToken /&gt; }}<span class="pl-pds">'</span></span>;</span>
<span class="pl-s1">    <span class="pl-k">var</span> map <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">mapboxgl.Map</span>({</span>
<span class="pl-s1">      container<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span>, <span class="pl-c"><span class="pl-c">//</span> Specify the container ID</span></span>
<span class="pl-s1">      style<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}<span class="pl-pds">'</span></span>, <span class="pl-c"><span class="pl-c">//</span> Specify which map style to use</span></span>
<span class="pl-s1">      center<span class="pl-k">:</span> [<span class="pl-k">-</span><span class="pl-c1">122.42136449</span>,<span class="pl-c1">37.80176523</span>], <span class="pl-c"><span class="pl-c">//</span> Specify the starting position</span></span>
<span class="pl-s1">      zoom<span class="pl-k">:</span> <span class="pl-c1">14.5</span>, <span class="pl-c"><span class="pl-c">//</span> Specify the starting zoom</span></span>
<span class="pl-s1">    });</span>
<span class="pl-s1">  </span>&lt;/<span class="pl-ent">script</span>&gt;
&lt;/<span class="pl-ent">body</span>&gt;

&lt;/<span class="pl-ent">html</span>&gt;</pre></div>
<p>This Mapbox GL JS code sets a style for the map, gives it coordinates on which to center, and sets a zoom level.</p>
<p>Save your changes. Open the HTML file in your browser to see the rendered map, which is centered on the city of San Francisco.</p>
<h2><a id="user-content-add-the-draw-tools" class="anchor" aria-hidden="true" href="#add-the-draw-tools"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add the Draw tools</h2>
<p>{{&lt;Note title="Options for passing coordinates to the Map Matching API" imageComponent={}&gt;}}</p>
<p>In this app created in this tutorial, the coordinates that the Map Matching API uses to generate a route are created by the user adding points directly to the map with the Mapbox GL Draw tools. Often, though, you would instead want to add the points used by the Map Matching API programmatically. For example, the Map Matching API could access a data set that contains landmark coordinates to create scenic routes, or a data set with the locations of known parking garages near the end of a route.</p>
<p>{{}}</p>
<p>The <a href="https://github.com/mapbox/mapbox-gl-draw">Mapbox GL Draw plugin</a> adds support for drawing features on maps created with Mapbox GL JS. In this step, you will add the Mapbox GL Draw <code>line_tool</code> and <code>trash</code> tools to your app, which will allow your users to draw lines and delete them. To add the draw tools, first add the links to the Mapbox GL Draw plugin's JavaScript and CSS to the head of the HTML file:</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;
&lt;<span class="pl-ent">link</span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">'</span>stylesheet<span class="pl-pds">'</span></span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.css<span class="pl-pds">'</span></span> <span class="pl-e">type</span>=<span class="pl-s"><span class="pl-pds">'</span>text/css<span class="pl-pds">'</span></span> /&gt;</pre></div>
<p>Once these links have been added, you will be able to use the Draw plugin in your app. When you add the Draw plugin, you can also specify the style of the line that gets drawn on the map when a user uses the draw tool. Add the following code above the closing <code>&lt;/script&gt;</code> tag in your HTML file.</p>
<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> draw <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">MapboxDraw</span>({
  <span class="pl-c"><span class="pl-c">//</span> Instead of showing all the draw tools, show only the line string and delete tools</span>
  displayControlsDefault<span class="pl-k">:</span> <span class="pl-c1">false</span>,
  controls<span class="pl-k">:</span> {
    line_string<span class="pl-k">:</span> <span class="pl-c1">true</span>,
    trash<span class="pl-k">:</span> <span class="pl-c1">true</span>
  },
  styles<span class="pl-k">:</span> [
    <span class="pl-c"><span class="pl-c">//</span> Set the line style for the user-input coordinates</span>
    {
      <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>gl-draw-line<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>line<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>filter<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-s"><span class="pl-pds">"</span>all<span class="pl-pds">"</span></span>, [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>$type<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>LineString<span class="pl-pds">"</span></span>],
        [<span class="pl-s"><span class="pl-pds">"</span>!=<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>mode<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>static<span class="pl-pds">"</span></span>]
      ],
      <span class="pl-s"><span class="pl-pds">"</span>layout<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
        <span class="pl-s"><span class="pl-pds">"</span>line-cap<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span>,
        <span class="pl-s"><span class="pl-pds">"</span>line-join<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span>
      },
      <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
        <span class="pl-s"><span class="pl-pds">"</span>line-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#438EE4<span class="pl-pds">"</span></span>,
        <span class="pl-s"><span class="pl-pds">"</span>line-dasharray<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-c1">0.2</span>, <span class="pl-c1">2</span>],
        <span class="pl-s"><span class="pl-pds">"</span>line-width<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">4</span>,
        <span class="pl-s"><span class="pl-pds">"</span>line-opacity<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">0.7</span>
      }
    },
    <span class="pl-c"><span class="pl-c">//</span> Style the vertex point halos</span>
    {
      <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>gl-draw-polygon-and-line-vertex-halo-active<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>circle<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>filter<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-s"><span class="pl-pds">"</span>all<span class="pl-pds">"</span></span>, [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>meta<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>vertex<span class="pl-pds">"</span></span>],
        [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>$type<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>Point<span class="pl-pds">"</span></span>],
        [<span class="pl-s"><span class="pl-pds">"</span>!=<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>mode<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>static<span class="pl-pds">"</span></span>]
      ],
      <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
        <span class="pl-s"><span class="pl-pds">"</span>circle-radius<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">12</span>,
        <span class="pl-s"><span class="pl-pds">"</span>circle-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#FFF<span class="pl-pds">"</span></span>
      }
    },
    <span class="pl-c"><span class="pl-c">//</span> Style the vertex points</span>
    {
      <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>gl-draw-polygon-and-line-vertex-active<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>circle<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>filter<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-s"><span class="pl-pds">"</span>all<span class="pl-pds">"</span></span>, [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>meta<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>vertex<span class="pl-pds">"</span></span>],
        [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>$type<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>Point<span class="pl-pds">"</span></span>],
        [<span class="pl-s"><span class="pl-pds">"</span>!=<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>mode<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>static<span class="pl-pds">"</span></span>]
      ],
      <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
        <span class="pl-s"><span class="pl-pds">"</span>circle-radius<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">8</span>,
        <span class="pl-s"><span class="pl-pds">"</span>circle-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#438EE4<span class="pl-pds">"</span></span>,
      }
    },
  ]
});

<span class="pl-c"><span class="pl-c">//</span> Add the draw tool to the map</span>
<span class="pl-smi">map</span>.<span class="pl-en">addControl</span>(draw);</pre></div>
<p>Save your file, then refresh the page in your browser. You will see icons for the specified Draw plugin controls, <code>line_tool</code> and <code>delete</code>, on the upper right side of the page. Click the <code>line_tool</code> icon. On the map, click once to start the line, then click one or more times to draw a path. When you're done drawing, click again on the last point to finish the path. The map will display a blue dashed line that follows the path you drew. For more information on how to style lines using this plugin, read the <a href="https://github.com/mapbox/mapbox-gl-draw/blob/master/docs/API.md#styling-draw">Styling Draw section</a> of the Mapbox GL Draw documentation.</p>
<p>In a few steps, you will link the code you wrote in this step with a function that takes this drawn path and gathers the coordinates to use in the Map Matching API call.</p>
<p>{{

}}</p>
<h2><a id="user-content-add-the-sidebar" class="anchor" aria-hidden="true" href="#add-the-sidebar"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add the sidebar</h2>
<p>Next, add a sidebar to the web app that will display instructions for users on how to use the app. This sidebar will also serve as a place to display turn-by-turn directions, which you will set up in a later step.</p>
<p>In the <code>&lt;body&gt;</code> of your HTML, add a new <code>&lt;div&gt;</code>. This <code>&lt;div&gt;</code> will hold the app's instructions and, later, the directions.</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>info-box<span class="pl-pds">"</span></span>&gt;
  &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">"</span>info<span class="pl-pds">"</span></span>&gt;
    &lt;<span class="pl-ent">p</span>&gt;Draw your route using the draw tools on the right. To get the most accurate route match, draw points at regular intervals.&lt;/<span class="pl-ent">p</span>&gt;
  &lt;/<span class="pl-ent">div</span>&gt;
  &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">"</span>directions<span class="pl-pds">"</span></span>&gt;&lt;/<span class="pl-ent">div</span>&gt;
&lt;/<span class="pl-ent">div</span>&gt;</pre></div>
<p>To style the new <code>&lt;div&gt;</code>, add the following CSS to the <code>&lt;style&gt;</code> section of your HTML:</p>
<div class="highlight highlight-source-css"><pre><span class="pl-e">.info-box</span> {
  <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;
  <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">25<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;
  <span class="pl-c1"><span class="pl-c1">bottom</span></span>: <span class="pl-c1">40<span class="pl-k">%</span></span>;
  <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">background-color</span></span>: <span class="pl-c1">rgba</span>(<span class="pl-c1">255</span>, <span class="pl-c1">255</span>, <span class="pl-c1">255</span>, <span class="pl-c1">0.9</span>);
  <span class="pl-c1"><span class="pl-c1">overflow-y</span></span>: <span class="pl-c1">scroll</span>;
  <span class="pl-c1"><span class="pl-c1">font-family</span></span>: <span class="pl-c1">sans-serif</span>;
  <span class="pl-c1"><span class="pl-c1">font-size</span></span>: <span class="pl-c1">0.8<span class="pl-k">em</span></span>;
  <span class="pl-c1"><span class="pl-c1">line-height</span></span>: <span class="pl-c1">2<span class="pl-k">em</span></span>;
}

<span class="pl-e">#info</span> {
  <span class="pl-c1"><span class="pl-c1">font-size</span></span>: <span class="pl-c1">16<span class="pl-k">px</span></span>;
  <span class="pl-c1"><span class="pl-c1">font-weight</span></span>: <span class="pl-c1">bold</span>;
}</pre></div>
<p>Save your work and refresh the page. The new information box will display on the left side of the page.</p>
<p>{{

}}</p>
<h2><a id="user-content-add-the-map-matching-api" class="anchor" aria-hidden="true" href="#add-the-map-matching-api"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add the Map Matching API</h2>
<p>A Map Matching API requires two parameters: the <code>profile</code> the query should use, and the <code>coordinates</code> that need to be matched to the OpenStreetMap road and path network. The <code>profile</code> can be either <code>walking</code>, <code>cycling</code>, <code>driving</code>, or <code>driving-traffic</code>. The <code>coordinates</code> are a semicolon-separated list of <code>{longitude},{latitude}</code> coordinate pairs to visit in order, of which there can be anywhere between two and 100.</p>
<pre><code>https://api.mapbox.com/matching/v5/mapbox/{profile}/{coordinates}.json?access_token=YOUR_MAPBOX_ACCESS_TOKEN
</code></pre>
<p>The Map Matching API also accepts several optional parameters that can be used to customize the query. For this app, you will be using two optional parameters:</p>
<ul>
<li><code>radiuses</code>: A semicolon-separated list that indicates the maximum distance a coordinate can be moved to snap to the road network in meters. Adding a radius tells the Map Matching API how precisely it must match the input coordinates, which may not always represent a location on the OpenStreetMap road network. The number of radiuses must be the same as the number of coordinates in the request.</li>
<li><code>steps</code>: Set to <code>true</code> to return step-by-step instructions.</li>
</ul>
<p>To learn more about the Map Matching API and its other optional parameters, explore the <a href="https://docs.mapbox.com/api/navigation/#map-matching" rel="nofollow">Map Matching API documentation</a>.</p>
<p>This example query uses the <code>driving</code> profile, has two coordinate pairs and two <code>radiuses</code>, and has the <code>steps</code> parameter set to <code>true</code>:</p>
<pre><code>https://api.mapbox.com/matching/v5/mapbox/driving/-117.17282,32.71204;-117.17288,32.71225?steps=true&amp;radiuses=25;25&amp;access_token={{ &lt;UserAccessToken /&gt; }}
</code></pre>
<p>A Map Matching API request that includes the <code>radiuses</code> and <code>steps</code> parameters returns a response that contains <code>matchings</code>, an array of match objects. A match object contains route leg objects, which give detailed information about each leg of the route, including the turn-by-turn directions. You will use the information returned by the Map Matching API to do two things: draw the matched route to the map, and return turn-by-turn directions.</p>
<p>To integrate the Map Matching API into your app, you will write two new functions, <code>updateRoute</code> and <code>getMatch</code>. <code>updateRoute</code> will take the coordinates from the user-generated line and format them so that they can be used in a Map Matching query. <code>getMatch</code> will construct the query string and will use Ajax to make the Map Matching API call. Used together, these two functions will make an API call using the coordinates drawn on the screen and will return the data necessary to complete the rest of the app. Add the following code to your JavaScript, before the closing <code>&lt;/script&gt;</code> tag:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> Use the coordinates you drew to make the Map Matching API request</span>
<span class="pl-k">function</span> <span class="pl-en">updateRoute</span>() {
  <span class="pl-c"><span class="pl-c">//</span> Set the profile</span>
  <span class="pl-k">var</span> profile <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>driving<span class="pl-pds">"</span></span>;
  <span class="pl-c"><span class="pl-c">//</span> Get the coordinates that were drawn on the map</span>
  <span class="pl-k">var</span> data <span class="pl-k">=</span> <span class="pl-smi">draw</span>.<span class="pl-c1">getAll</span>();
  <span class="pl-k">var</span> lastFeature <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">features</span>.<span class="pl-c1">length</span> <span class="pl-k">-</span> <span class="pl-c1">1</span>;
  <span class="pl-k">var</span> coords <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">features</span>[lastFeature].<span class="pl-smi">geometry</span>.<span class="pl-smi">coordinates</span>;
  <span class="pl-c"><span class="pl-c">//</span> Format the coordinates</span>
  <span class="pl-k">var</span> newCoords <span class="pl-k">=</span> <span class="pl-smi">coords</span>.<span class="pl-c1">join</span>(<span class="pl-s"><span class="pl-pds">'</span>;<span class="pl-pds">'</span></span>)
  <span class="pl-c"><span class="pl-c">//</span> Set the radius for each coordinate pair to 25 meters</span>
  <span class="pl-k">var</span> radius <span class="pl-k">=</span> [];
  <span class="pl-smi">coords</span>.<span class="pl-c1">forEach</span>(<span class="pl-smi">element</span> <span class="pl-k">=&gt;</span> {
    <span class="pl-smi">radius</span>.<span class="pl-c1">push</span>(<span class="pl-c1">25</span>);
  });
  <span class="pl-en">getMatch</span>(newCoords, radius, profile);
}

<span class="pl-c"><span class="pl-c">//</span> Make a Map Matching request</span>
<span class="pl-k">function</span> <span class="pl-en">getMatch</span>(<span class="pl-smi">coordinates</span>, <span class="pl-smi">radius</span>, <span class="pl-smi">profile</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Separate the radiuses with semicolons</span>
  <span class="pl-k">var</span> radiuses <span class="pl-k">=</span> <span class="pl-smi">radius</span>.<span class="pl-c1">join</span>(<span class="pl-s"><span class="pl-pds">'</span>;<span class="pl-pds">'</span></span>)
  <span class="pl-c"><span class="pl-c">//</span> Create the query</span>
  <span class="pl-k">var</span> query <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/matching/v5/mapbox/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> profile <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> coordinates <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>?geometries=geojson&amp;radiuses=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> radiuses <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&amp;steps=true&amp;access_token=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span>;

  <span class="pl-smi">$</span>.<span class="pl-en">ajax</span>({
    method<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>GET<span class="pl-pds">'</span></span>,
    url<span class="pl-k">:</span> query
  }).<span class="pl-en">done</span>(<span class="pl-k">function</span>(<span class="pl-smi">data</span>) {
    <span class="pl-c"><span class="pl-c">//</span> Get the coordinates from the response</span>
    <span class="pl-k">var</span> coords <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">matchings</span>[<span class="pl-c1">0</span>].<span class="pl-smi">geometry</span>;
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(coords);
    <span class="pl-c"><span class="pl-c">//</span> Code from the next step will go here</span>
  });
}</pre></div>
<p>By calling the <code>getMatch</code> function in <code>updateRoute</code>, you can access the user-drawn coordinates and use them as the coordinates in the Map Matching API call. In the next step you will add a new drawn line to show the matched route, but for now you can view the coordinate results using <code>console.log()</code>.</p>
<p>To call <code>getMatch</code> when your user draws or updates a line on the map, add the following lines before the closing <code>&lt;/script&gt;</code> tag:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>draw.create<span class="pl-pds">'</span></span>, updateRoute);
<span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>draw.update<span class="pl-pds">'</span></span>, updateRoute);</pre></div>
<p>Save your work, then refresh your browser page and open the browser's developer tools. When you draw a route on the map, your app will print the coordinate data returned by the Map Matching API to the JavaScript console.</p>
<p>{{

}}</p>
<h2><a id="user-content-draw-the-map-matching-route" class="anchor" aria-hidden="true" href="#draw-the-map-matching-route"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Draw the Map Matching route</h2>
<p>Next, you will create an <code>addRoute</code> function that takes the coordinates returned by the Map Matching API and adds them on the map as a new layer. Paste the following code into your JavaScript, above the final <code>&lt;/script&gt;</code> tag:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> Draw the Map Matching route as a new layer on the map</span>
<span class="pl-k">function</span> <span class="pl-en">addRoute</span>(<span class="pl-smi">coords</span>) {
  <span class="pl-c"><span class="pl-c">//</span> If a route is already loaded, remove it</span>
  <span class="pl-k">if</span> (<span class="pl-smi">map</span>.<span class="pl-en">getSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)) {
    <span class="pl-smi">map</span>.<span class="pl-en">removeLayer</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)
    <span class="pl-smi">map</span>.<span class="pl-en">removeSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)
  } <span class="pl-k">else</span> { <span class="pl-c"><span class="pl-c">//</span> Add a new layer to the map</span>
    <span class="pl-smi">map</span>.<span class="pl-en">addLayer</span>({
      <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>route<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>line<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>source<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
        <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>geojson<span class="pl-pds">"</span></span>,
        <span class="pl-s"><span class="pl-pds">"</span>data<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
          <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>Feature<span class="pl-pds">"</span></span>,
          <span class="pl-s"><span class="pl-pds">"</span>properties<span class="pl-pds">"</span></span><span class="pl-k">:</span> {},
          <span class="pl-s"><span class="pl-pds">"</span>geometry<span class="pl-pds">"</span></span><span class="pl-k">:</span> coords
        }
      },
      <span class="pl-s"><span class="pl-pds">"</span>layout<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
        <span class="pl-s"><span class="pl-pds">"</span>line-join<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span>,
        <span class="pl-s"><span class="pl-pds">"</span>line-cap<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span>
      },
      <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {
        <span class="pl-s"><span class="pl-pds">"</span>line-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#03AA46<span class="pl-pds">"</span></span>,
        <span class="pl-s"><span class="pl-pds">"</span>line-width<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">8</span>,
        <span class="pl-s"><span class="pl-pds">"</span>line-opacity<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">0.8</span>
      }
    });
  };
}</pre></div>
<p>Call <code>addRoute</code> within your <code>getRoute</code> function so that it can access the coordinates returned by the Map Matching API. <code>getRoute</code> will now look like this:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> Make a Map Matching request</span>
<span class="pl-k">function</span> <span class="pl-en">getMatch</span>(<span class="pl-smi">coordinates</span>, <span class="pl-smi">radius</span>, <span class="pl-smi">profile</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Separate the radiuses with semicolons</span>
  <span class="pl-k">var</span> radiuses <span class="pl-k">=</span> <span class="pl-smi">radius</span>.<span class="pl-c1">join</span>(<span class="pl-s"><span class="pl-pds">'</span>;<span class="pl-pds">'</span></span>)
  <span class="pl-c"><span class="pl-c">//</span> Create the query</span>
  <span class="pl-k">var</span> query <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/matching/v5/mapbox/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> profile <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> coordinates <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>?geometries=geojson&amp;radiuses=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> radiuses <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&amp;steps=true&amp;access_token=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span>;
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(query)
  <span class="pl-smi">$</span>.<span class="pl-en">ajax</span>({
    method<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>GET<span class="pl-pds">'</span></span>,
    url<span class="pl-k">:</span> query
  }).<span class="pl-en">done</span>(<span class="pl-k">function</span>(<span class="pl-smi">data</span>) {
    <span class="pl-c"><span class="pl-c">//</span> Get the coordinates from the response</span>
    <span class="pl-k">var</span> coords <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">matchings</span>[<span class="pl-c1">0</span>].<span class="pl-smi">geometry</span>;
    <span class="pl-c"><span class="pl-c">//</span> Draw the route on the map</span>
    <span class="pl-en">addRoute</span>(coords);
  });
}</pre></div>
<p>Save your changes and refresh the browser page. Now when you use the <code>line_draw</code> tool to trace a route, the route generated by the Map Matching API also shows on the map. As you can see, the line drawn by the user won't always match up directly with the route generated by the Map Matching API. This is because the Map Matching API takes the input coordinates, which may not be located directly on the road network, and snaps them to the nearest road within the 25 meter radius that you specified in the <code>radiuses</code> parameter.</p>
<p>{{

}}</p>
<h2><a id="user-content-display-the-turn-by-turn-directions" class="anchor" aria-hidden="true" href="#display-the-turn-by-turn-directions"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display the turn-by-turn directions</h2>
<p>Now it's time to add the turn-by-turn instructions from the Map Matching API to the sidebar! Doing so requires writing a new function, <code>getInstructions</code>, that will allow you to dig down into the Map Matching API response object to get the information you need: the total time that the route will take, and the maneuver instructions for each step of the route. (Read more about what gets returned in the Map Matching API's route step object in the <a href="https://docs.mapbox.com/api/navigation/#route-step-object" rel="nofollow">Map Matching API documentation</a>.) Add the following code to the JavaScript, below the <code>getMatch</code> method:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">getInstructions</span>(<span class="pl-smi">data</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Target the sidebar to add the instructions</span>
  <span class="pl-k">var</span> directions <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementById</span>(<span class="pl-s"><span class="pl-pds">'</span>directions<span class="pl-pds">'</span></span>);

  <span class="pl-k">var</span> legs <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">legs</span>;
  <span class="pl-k">var</span> tripDirections <span class="pl-k">=</span> [];
  <span class="pl-c"><span class="pl-c">//</span> Output the instructions for each step of each leg in the response object</span>
  <span class="pl-k">for</span> (<span class="pl-k">var</span> i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k">&lt;</span> <span class="pl-smi">legs</span>.<span class="pl-c1">length</span>; i<span class="pl-k">++</span>) {
    <span class="pl-k">var</span> steps <span class="pl-k">=</span> legs[i].<span class="pl-smi">steps</span>;
    <span class="pl-k">for</span> (<span class="pl-k">var</span> j <span class="pl-k">=</span> <span class="pl-c1">0</span>; j <span class="pl-k">&lt;</span> <span class="pl-smi">steps</span>.<span class="pl-c1">length</span>; j<span class="pl-k">++</span>) {
      <span class="pl-smi">tripDirections</span>.<span class="pl-c1">push</span>(<span class="pl-s"><span class="pl-pds">'</span>&lt;br&gt;&lt;li&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span> steps[j].<span class="pl-smi">maneuver</span>.<span class="pl-smi">instruction</span>) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;/li&gt;<span class="pl-pds">'</span></span>;
    }
  }
  <span class="pl-smi">directions</span>.<span class="pl-smi">innerHTML</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;br&gt;&lt;h2&gt;Trip duration: <span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-c1">Math</span>.<span class="pl-c1">floor</span>(<span class="pl-smi">data</span>.<span class="pl-smi">duration</span> <span class="pl-k">/</span> <span class="pl-c1">60</span>) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span> min.&lt;/h2&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span> tripDirections;
}</pre></div>
<p>Next, call <code>getInstructions</code> within your <code>getRoute</code> function so that it can access the data returned by the Map Matching API. <code>getRoute</code> will now look like this:</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> Make a Map Matching request</span>
<span class="pl-k">function</span> <span class="pl-en">getMatch</span>(<span class="pl-smi">coordinates</span>, <span class="pl-smi">radius</span>, <span class="pl-smi">profile</span>) {
  <span class="pl-c"><span class="pl-c">//</span> Separate the radiuses with semicolons</span>
  <span class="pl-k">var</span> radiuses <span class="pl-k">=</span> <span class="pl-smi">radius</span>.<span class="pl-c1">join</span>(<span class="pl-s"><span class="pl-pds">'</span>;<span class="pl-pds">'</span></span>)
  <span class="pl-c"><span class="pl-c">//</span> Create the query</span>
  <span class="pl-k">var</span> query <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/matching/v5/mapbox/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> profile <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> coordinates <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>?geometries=geojson&amp;radiuses=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> radiuses <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&amp;steps=true&amp;access_token=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span>;
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(query)
  <span class="pl-smi">$</span>.<span class="pl-en">ajax</span>({
    method<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>GET<span class="pl-pds">'</span></span>,
    url<span class="pl-k">:</span> query
  }).<span class="pl-en">done</span>(<span class="pl-k">function</span>(<span class="pl-smi">data</span>) {
    <span class="pl-k">var</span> coords <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">matchings</span>[<span class="pl-c1">0</span>].<span class="pl-smi">geometry</span>;
    <span class="pl-c"><span class="pl-c">//</span> Draw the route on the map</span>
    <span class="pl-en">addRoute</span>(coords);
    <span class="pl-en">getInstructions</span>(<span class="pl-smi">data</span>.<span class="pl-smi">matchings</span>[<span class="pl-c1">0</span>]);
  });
}</pre></div>
<p>Save your changes and refresh your browser page. Now when you draw a route on the map, you will see the trip duration and the turn-by-turn instructions in the sidebar.</p>
<p>{{

}}</p>
<h2><a id="user-content-let-users-delete-a-route" class="anchor" aria-hidden="true" href="#let-users-delete-a-route"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Let users delete a route</h2>
<p>The last step is to add a function that allows your users to delete a route they have drawn on the map.</p>
<div class="highlight highlight-source-js"><pre><span class="pl-c"><span class="pl-c">//</span> If the user clicks the delete draw button, remove the layer if it exists</span>
<span class="pl-k">function</span> <span class="pl-en">removeRoute</span>() {
  <span class="pl-k">if</span> (<span class="pl-smi">map</span>.<span class="pl-en">getSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)) {
    <span class="pl-smi">map</span>.<span class="pl-en">removeLayer</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>);
    <span class="pl-smi">map</span>.<span class="pl-en">removeSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>);
  } <span class="pl-k">else</span> {
    <span class="pl-k">return</span>;
  }
}</pre></div>
<p>To connect the <code>removeRoute</code> function with the Mapbox GL Draw plugin's delete button, add the following line to your JavaScript:</p>
<div class="highlight highlight-source-js"><pre>  <span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>draw.delete<span class="pl-pds">'</span></span>, removeRoute);</pre></div>
<p>Save your work and refresh the browser page. When you draw a line and then click the Draw plugin's delete button, the line is removed from the page.</p>
<h2><a id="user-content-final-product" class="anchor" aria-hidden="true" href="#final-product"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Final product</h2>
<p>You have created an app that uses the Mapbox Map Matching API to snap user-provided coordinates to the road network, while at the same time displaying the route on a map and showing users the turn-by-turn instructions for the route.</p>
<p>{{

}}</p>
<p>The final HTML file will look like the following:</p>
<div class="highlight highlight-text-html-basic"><pre>&lt;!DOCTYPE html&gt;
&lt;<span class="pl-ent">html</span>&gt;

&lt;<span class="pl-ent">head</span>&gt;
  &lt;<span class="pl-ent">meta</span> <span class="pl-e">charset</span>=<span class="pl-s"><span class="pl-pds">'</span>utf-8<span class="pl-pds">'</span></span> /&gt;
  &lt;<span class="pl-ent">title</span>&gt;Get started with the Map Matching API&lt;/<span class="pl-ent">title</span>&gt;
  &lt;<span class="pl-ent">meta</span> <span class="pl-e">name</span>=<span class="pl-s"><span class="pl-pds">'</span>viewport<span class="pl-pds">'</span></span> <span class="pl-e">content</span>=<span class="pl-s"><span class="pl-pds">'</span>initial-scale=1,maximum-scale=1,user-scalable=no<span class="pl-pds">'</span></span> /&gt;
  <span class="pl-c"><span class="pl-c">&lt;!--</span> Import Mapbox GL JS  <span class="pl-c">--&gt;</span></span>
  &lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;
  &lt;<span class="pl-ent">link</span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css<span class="pl-pds">'</span></span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">'</span>stylesheet<span class="pl-pds">'</span></span> /&gt;
  <span class="pl-c"><span class="pl-c">&lt;!--</span> Import jQuery <span class="pl-c">--&gt;</span></span>
  &lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;
  <span class="pl-c"><span class="pl-c">&lt;!--</span> Import Mapbox GL Draw <span class="pl-c">--&gt;</span></span>
  &lt;<span class="pl-ent">script</span> <span class="pl-e">src</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.js<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">script</span>&gt;
  &lt;<span class="pl-ent">link</span> <span class="pl-e">rel</span>=<span class="pl-s"><span class="pl-pds">'</span>stylesheet<span class="pl-pds">'</span></span> <span class="pl-e">href</span>=<span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.css<span class="pl-pds">'</span></span> <span class="pl-e">type</span>=<span class="pl-s"><span class="pl-pds">'</span>text/css<span class="pl-pds">'</span></span> /&gt;

  &lt;<span class="pl-ent">style</span>&gt;<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-ent">body</span> {</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-e">#map</span> {</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">bottom</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">100<span class="pl-k">%</span></span>;</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-e">.info-box</span> {</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">position</span></span>: <span class="pl-c1">absolute</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">margin</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">width</span></span>: <span class="pl-c1">25<span class="pl-k">%</span></span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">top</span></span>: <span class="pl-c1">0</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">bottom</span></span>: <span class="pl-c1">40<span class="pl-k">%</span></span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">padding</span></span>: <span class="pl-c1">20<span class="pl-k">px</span></span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">background-color</span></span>: <span class="pl-c1">rgba</span>(<span class="pl-c1">255</span>, <span class="pl-c1">255</span>, <span class="pl-c1">255</span>, <span class="pl-c1">0.9</span>);</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">overflow-y</span></span>: <span class="pl-c1">scroll</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">font-family</span></span>: <span class="pl-c1">sans-serif</span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">font-size</span></span>: <span class="pl-c1">0.8<span class="pl-k">em</span></span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">line-height</span></span>: <span class="pl-c1">2<span class="pl-k">em</span></span>;</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-e">#info</span> {</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">font-size</span></span>: <span class="pl-c1">16<span class="pl-k">px</span></span>;</span>
<span class="pl-s1">      <span class="pl-c1"><span class="pl-c1">font-weight</span></span>: <span class="pl-c1">bold</span>;</span>
<span class="pl-s1">    }</span>
<span class="pl-s1">  </span>&lt;/<span class="pl-ent">style</span>&gt;
&lt;/<span class="pl-ent">head</span>&gt;

&lt;<span class="pl-ent">body</span>&gt;
  <span class="pl-c"><span class="pl-c">&lt;!--</span> Create a container for the map <span class="pl-c">--&gt;</span></span>
  &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span>&gt;&lt;/<span class="pl-ent">div</span>&gt;

  &lt;<span class="pl-ent">div</span> <span class="pl-e">class</span>=<span class="pl-s"><span class="pl-pds">"</span>info-box<span class="pl-pds">"</span></span>&gt;
    &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">"</span>info<span class="pl-pds">"</span></span>&gt;
      &lt;<span class="pl-ent">p</span>&gt;Draw your route using the draw tools on the right. To get the most accurate route match, draw points at regular intervals.&lt;/<span class="pl-ent">p</span>&gt;
    &lt;/<span class="pl-ent">div</span>&gt;
    &lt;<span class="pl-ent">div</span> <span class="pl-e">id</span>=<span class="pl-s"><span class="pl-pds">"</span>directions<span class="pl-pds">"</span></span>&gt;&lt;/<span class="pl-ent">div</span>&gt;
  &lt;/<span class="pl-ent">div</span>&gt;

  &lt;<span class="pl-ent">script</span>&gt;<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-c"><span class="pl-c">//</span> Add your Mapbox access token</span></span>
<span class="pl-s1">    <span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>{{ &lt;UserAccessToken/&gt; }}<span class="pl-pds">'</span></span>;</span>
<span class="pl-s1">    <span class="pl-k">var</span> map <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">mapboxgl.Map</span>({</span>
<span class="pl-s1">      container<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>map<span class="pl-pds">'</span></span>, <span class="pl-c"><span class="pl-c">//</span> Specify the container ID</span></span>
<span class="pl-s1">      style<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}<span class="pl-pds">'</span></span>, <span class="pl-c"><span class="pl-c">//</span> Specify which map style to use</span></span>
<span class="pl-s1">      center<span class="pl-k">:</span> [<span class="pl-k">-</span><span class="pl-c1">122.42136449</span>,<span class="pl-c1">37.80176523</span>], <span class="pl-c"><span class="pl-c">//</span> Specify the starting position</span></span>
<span class="pl-s1">      zoom<span class="pl-k">:</span> <span class="pl-c1">14.5</span>, <span class="pl-c"><span class="pl-c">//</span> Specify the starting zoom</span></span>
<span class="pl-s1">    });</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-k">var</span> draw <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">MapboxDraw</span>({</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Instead of showing all the draw tools, show only the line string and delete tools</span></span>
<span class="pl-s1">      displayControlsDefault<span class="pl-k">:</span> <span class="pl-c1">false</span>,</span>
<span class="pl-s1">      controls<span class="pl-k">:</span> {</span>
<span class="pl-s1">        line_string<span class="pl-k">:</span> <span class="pl-c1">true</span>,</span>
<span class="pl-s1">        trash<span class="pl-k">:</span> <span class="pl-c1">true</span></span>
<span class="pl-s1">      },</span>
<span class="pl-s1">      styles<span class="pl-k">:</span> [</span>
<span class="pl-s1">        <span class="pl-c"><span class="pl-c">//</span> Set the line style for the user-input coordinates</span></span>
<span class="pl-s1">        {</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>gl-draw-line<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>line<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>filter<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-s"><span class="pl-pds">"</span>all<span class="pl-pds">"</span></span>, [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>$type<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>LineString<span class="pl-pds">"</span></span>],</span>
<span class="pl-s1">            [<span class="pl-s"><span class="pl-pds">"</span>!=<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>mode<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>static<span class="pl-pds">"</span></span>]</span>
<span class="pl-s1">          ],</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>layout<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-cap<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-join<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span></span>
<span class="pl-s1">          },</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#438EE4<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-dasharray<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-c1">0.2</span>, <span class="pl-c1">2</span>],</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-width<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">4</span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-opacity<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">0.7</span></span>
<span class="pl-s1">          }</span>
<span class="pl-s1">        },</span>
<span class="pl-s1">        <span class="pl-c"><span class="pl-c">//</span> Style the vertex point halos</span></span>
<span class="pl-s1">        {</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>gl-draw-polygon-and-line-vertex-halo-active<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>circle<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>filter<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-s"><span class="pl-pds">"</span>all<span class="pl-pds">"</span></span>, [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>meta<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>vertex<span class="pl-pds">"</span></span>],</span>
<span class="pl-s1">            [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>$type<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>Point<span class="pl-pds">"</span></span>],</span>
<span class="pl-s1">            [<span class="pl-s"><span class="pl-pds">"</span>!=<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>mode<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>static<span class="pl-pds">"</span></span>]</span>
<span class="pl-s1">          ],</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>circle-radius<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">12</span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>circle-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#FFF<span class="pl-pds">"</span></span></span>
<span class="pl-s1">          }</span>
<span class="pl-s1">        },</span>
<span class="pl-s1">        <span class="pl-c"><span class="pl-c">//</span> Style the vertex points</span></span>
<span class="pl-s1">        {</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>gl-draw-polygon-and-line-vertex-active<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>circle<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>filter<span class="pl-pds">"</span></span><span class="pl-k">:</span> [<span class="pl-s"><span class="pl-pds">"</span>all<span class="pl-pds">"</span></span>, [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>meta<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>vertex<span class="pl-pds">"</span></span>],</span>
<span class="pl-s1">            [<span class="pl-s"><span class="pl-pds">"</span>==<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>$type<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>Point<span class="pl-pds">"</span></span>],</span>
<span class="pl-s1">            [<span class="pl-s"><span class="pl-pds">"</span>!=<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>mode<span class="pl-pds">"</span></span>, <span class="pl-s"><span class="pl-pds">"</span>static<span class="pl-pds">"</span></span>]</span>
<span class="pl-s1">          ],</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>circle-radius<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">8</span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>circle-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#438EE4<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          }</span>
<span class="pl-s1">        },</span>
<span class="pl-s1">      ]</span>
<span class="pl-s1">    });</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-c"><span class="pl-c">//</span> Add the draw tool to the map</span></span>
<span class="pl-s1">    <span class="pl-smi">map</span>.<span class="pl-en">addControl</span>(draw);</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-k">function</span> <span class="pl-en">updateRoute</span>() {</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Set the profile</span></span>
<span class="pl-s1">      <span class="pl-k">var</span> profile <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>driving<span class="pl-pds">"</span></span>;</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Get the coordinates that were drawn on the map</span></span>
<span class="pl-s1">      <span class="pl-k">var</span> data <span class="pl-k">=</span> <span class="pl-smi">draw</span>.<span class="pl-c1">getAll</span>();</span>
<span class="pl-s1">      <span class="pl-k">var</span> lastFeature <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">features</span>.<span class="pl-c1">length</span> <span class="pl-k">-</span> <span class="pl-c1">1</span>;</span>
<span class="pl-s1">      <span class="pl-k">var</span> coords <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">features</span>[lastFeature].<span class="pl-smi">geometry</span>.<span class="pl-smi">coordinates</span>;</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Format the coordinates</span></span>
<span class="pl-s1">      <span class="pl-k">var</span> newCoords <span class="pl-k">=</span> <span class="pl-smi">coords</span>.<span class="pl-c1">join</span>(<span class="pl-s"><span class="pl-pds">'</span>;<span class="pl-pds">'</span></span>)</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Set the radius for each coordinate pair to 25 meters</span></span>
<span class="pl-s1">      <span class="pl-k">var</span> radius <span class="pl-k">=</span> [];</span>
<span class="pl-s1">      <span class="pl-smi">coords</span>.<span class="pl-c1">forEach</span>(<span class="pl-smi">element</span> <span class="pl-k">=&gt;</span> {</span>
<span class="pl-s1">        <span class="pl-smi">radius</span>.<span class="pl-c1">push</span>(<span class="pl-c1">25</span>);</span>
<span class="pl-s1">      });</span>
<span class="pl-s1">      <span class="pl-en">getMatch</span>(newCoords, radius, profile);</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-c"><span class="pl-c">//</span> Make a Map Matching request</span></span>
<span class="pl-s1">    <span class="pl-k">function</span> <span class="pl-en">getMatch</span>(<span class="pl-smi">coordinates</span>, <span class="pl-smi">radius</span>, <span class="pl-smi">profile</span>) {</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Separate the radiuses with semicolons</span></span>
<span class="pl-s1">      <span class="pl-k">var</span> radiuses <span class="pl-k">=</span> <span class="pl-smi">radius</span>.<span class="pl-c1">join</span>(<span class="pl-s"><span class="pl-pds">'</span>;<span class="pl-pds">'</span></span>)</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Create the query</span></span>
<span class="pl-s1">      <span class="pl-k">var</span> query <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>https://api.mapbox.com/matching/v5/mapbox/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> profile <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>/<span class="pl-pds">'</span></span> <span class="pl-k">+</span> coordinates <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>?geometries=geojson&amp;radiuses=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> radiuses <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&amp;steps=true&amp;access_token=<span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-smi">mapboxgl</span>.<span class="pl-smi">accessToken</span>;</span>
<span class="pl-s1"></span>
<span class="pl-s1">      <span class="pl-smi">$</span>.<span class="pl-en">ajax</span>({</span>
<span class="pl-s1">        method<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>GET<span class="pl-pds">'</span></span>,</span>
<span class="pl-s1">        url<span class="pl-k">:</span> query</span>
<span class="pl-s1">      }).<span class="pl-en">done</span>(<span class="pl-k">function</span>(<span class="pl-smi">data</span>) {</span>
<span class="pl-s1">        <span class="pl-c"><span class="pl-c">//</span> Get the coordinates from the response</span></span>
<span class="pl-s1">        <span class="pl-k">var</span> coords <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">matchings</span>[<span class="pl-c1">0</span>].<span class="pl-smi">geometry</span>;</span>
<span class="pl-s1">        <span class="pl-c"><span class="pl-c">//</span> Draw the route on the map</span></span>
<span class="pl-s1">        <span class="pl-en">addRoute</span>(coords);</span>
<span class="pl-s1">        <span class="pl-en">getInstructions</span>(<span class="pl-smi">data</span>.<span class="pl-smi">matchings</span>[<span class="pl-c1">0</span>]);</span>
<span class="pl-s1">      });</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-c"><span class="pl-c">//</span> Draw the Map Matching route as a new layer on the map</span></span>
<span class="pl-s1">    <span class="pl-k">function</span> <span class="pl-en">addRoute</span>(<span class="pl-smi">coords</span>) {</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> If a route is already loaded, remove it</span></span>
<span class="pl-s1">      <span class="pl-k">if</span> (<span class="pl-smi">map</span>.<span class="pl-en">getSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)) {</span>
<span class="pl-s1">        <span class="pl-smi">map</span>.<span class="pl-en">removeLayer</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)</span>
<span class="pl-s1">        <span class="pl-smi">map</span>.<span class="pl-en">removeSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)</span>
<span class="pl-s1">      } <span class="pl-k">else</span> {</span>
<span class="pl-s1">        <span class="pl-smi">map</span>.<span class="pl-en">addLayer</span>({</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>id<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>route<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>line<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>source<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>geojson<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>data<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">              <span class="pl-s"><span class="pl-pds">"</span>type<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>Feature<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">              <span class="pl-s"><span class="pl-pds">"</span>properties<span class="pl-pds">"</span></span><span class="pl-k">:</span> {},</span>
<span class="pl-s1">              <span class="pl-s"><span class="pl-pds">"</span>geometry<span class="pl-pds">"</span></span><span class="pl-k">:</span> coords</span>
<span class="pl-s1">            }</span>
<span class="pl-s1">          },</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>layout<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-join<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-cap<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>round<span class="pl-pds">"</span></span></span>
<span class="pl-s1">          },</span>
<span class="pl-s1">          <span class="pl-s"><span class="pl-pds">"</span>paint<span class="pl-pds">"</span></span><span class="pl-k">:</span> {</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-color<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">"</span>#03AA46<span class="pl-pds">"</span></span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-width<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">8</span>,</span>
<span class="pl-s1">            <span class="pl-s"><span class="pl-pds">"</span>line-opacity<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-c1">0.8</span></span>
<span class="pl-s1">          }</span>
<span class="pl-s1">        });</span>
<span class="pl-s1">      };</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-k">function</span> <span class="pl-en">getInstructions</span>(<span class="pl-smi">data</span>) {</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Target the sidebar to add the instructions</span></span>
<span class="pl-s1">      <span class="pl-k">var</span> directions <span class="pl-k">=</span> <span class="pl-c1">document</span>.<span class="pl-c1">getElementById</span>(<span class="pl-s"><span class="pl-pds">'</span>directions<span class="pl-pds">'</span></span>);</span>
<span class="pl-s1"></span>
<span class="pl-s1">      <span class="pl-k">var</span> legs <span class="pl-k">=</span> <span class="pl-smi">data</span>.<span class="pl-smi">legs</span>;</span>
<span class="pl-s1">      <span class="pl-k">var</span> tripDirections <span class="pl-k">=</span> [];</span>
<span class="pl-s1">      <span class="pl-c"><span class="pl-c">//</span> Output the instructions for each step of each leg in the response object</span></span>
<span class="pl-s1">      <span class="pl-k">for</span> (<span class="pl-k">var</span> i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k">&lt;</span> <span class="pl-smi">legs</span>.<span class="pl-c1">length</span>; i<span class="pl-k">++</span>) {</span>
<span class="pl-s1">        <span class="pl-k">var</span> steps <span class="pl-k">=</span> legs[i].<span class="pl-smi">steps</span>;</span>
<span class="pl-s1">        <span class="pl-k">for</span> (<span class="pl-k">var</span> j <span class="pl-k">=</span> <span class="pl-c1">0</span>; j <span class="pl-k">&lt;</span> <span class="pl-smi">steps</span>.<span class="pl-c1">length</span>; j<span class="pl-k">++</span>) {</span>
<span class="pl-s1">          <span class="pl-smi">tripDirections</span>.<span class="pl-c1">push</span>(<span class="pl-s"><span class="pl-pds">'</span>&lt;br&gt;&lt;li&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span> steps[j].<span class="pl-smi">maneuver</span>.<span class="pl-smi">instruction</span>) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;/li&gt;<span class="pl-pds">'</span></span>;</span>
<span class="pl-s1">        }</span>
<span class="pl-s1">      }</span>
<span class="pl-s1">      <span class="pl-smi">directions</span>.<span class="pl-smi">innerHTML</span> <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;br&gt;&lt;h2&gt;Trip duration: <span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-c1">Math</span>.<span class="pl-c1">floor</span>(<span class="pl-smi">data</span>.<span class="pl-smi">duration</span> <span class="pl-k">/</span> <span class="pl-c1">60</span>) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span> min.&lt;/h2&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span> tripDirections;</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-c"><span class="pl-c">//</span> If the user clicks the delete draw button, remove the layer if it exists</span></span>
<span class="pl-s1">    <span class="pl-k">function</span> <span class="pl-en">removeRoute</span>() {</span>
<span class="pl-s1">      <span class="pl-k">if</span> (<span class="pl-smi">map</span>.<span class="pl-en">getSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>)) {</span>
<span class="pl-s1">        <span class="pl-smi">map</span>.<span class="pl-en">removeLayer</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>);</span>
<span class="pl-s1">        <span class="pl-smi">map</span>.<span class="pl-en">removeSource</span>(<span class="pl-s"><span class="pl-pds">'</span>route<span class="pl-pds">'</span></span>);</span>
<span class="pl-s1">      } <span class="pl-k">else</span> {</span>
<span class="pl-s1">        <span class="pl-k">return</span>;</span>
<span class="pl-s1">      }</span>
<span class="pl-s1">    }</span>
<span class="pl-s1"></span>
<span class="pl-s1">    <span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>draw.create<span class="pl-pds">'</span></span>, updateRoute);</span>
<span class="pl-s1">    <span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>draw.update<span class="pl-pds">'</span></span>, updateRoute);</span>
<span class="pl-s1">    <span class="pl-smi">map</span>.<span class="pl-en">on</span>(<span class="pl-s"><span class="pl-pds">'</span>draw.delete<span class="pl-pds">'</span></span>, removeRoute);</span>
<span class="pl-s1">  </span>&lt;/<span class="pl-ent">script</span>&gt;
&lt;/<span class="pl-ent">body</span>&gt;

&lt;/<span class="pl-ent">html</span>&gt;
</pre></div>
<h2><a id="user-content-next-steps" class="anchor" aria-hidden="true" href="#next-steps"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Next steps</h2>
<p>To build on top of the tools and techniques you used in this tutorial, explore the following resources:</p>
<ul>
<li>Learn more about how you can use the Map Matching API's optional parameters to influence what gets returned in the response object in the <a href="https://docs.mapbox.com/api/navigation/#map-matching" rel="nofollow">Map Matching API documentation</a>.</li>
<li>Learn more about adding layers to a map using Mapbox GL JS in the <a href="https://docs.mapbox.com/mapbox-gl-js/example/geojson-line/" rel="nofollow">Add a GeoJSON line example</a> and in the <a href="https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer" rel="nofollow"><code>addLayer</code> documentation</a>.</li>
<li>Learn more about how to use the Mapbox GL Draw plugin in the <a href="https://docs.mapbox.com/mapbox-gl-js/example/mapbox-gl-draw/" rel="nofollow">Show drawn polygon area example</a> and in the <a href="https://github.com/mapbox/mapbox-gl-draw/tree/master/docs">Mapbox GL Draw plugin documentation</a>.</li>
</ul>
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
      <li class="mr-3 mr-lg-0">&copy; 2019 <span title="0.86257s from unicorn-5b9858554-w4vwk">GitHub</span>, Inc.</li>
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

