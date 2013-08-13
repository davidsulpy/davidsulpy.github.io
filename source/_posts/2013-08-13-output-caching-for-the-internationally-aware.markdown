---
layout: post
title: "Output Caching for the Internationally Aware"
date: 2013-08-13 10:27
comments: true
categories: [outputcaching, caching, asp.net]
---

Output caching is highly recommended for high traffic sites. Microsoft offers output caching out of the box for MVC applications through the `System.Web.Mvc` namespace. With the `OutputCache` attribute class you can specify certain MVC actions on a controller to return cached outputs. This will greatly reduce server load and improve responstime for large scale applications.

However, whole-section or whole-page output caching for a server-side dynamic site doesn't meet everyone's needs out of the box. What if you have certain areas of your site that are user-specific dynamic and, more importantly, have pii that should at least be prevented by accidental access from another user? Enter, donut hole caching, or donut caching. This allows the caching of just specific areas of a site (donut hole caching) or excluding specific areas from cache (donut caching) so you don't cache areas such as the login information in the top right corner of a page to be viewed by anyone.

DevTrends created a great library for donut caching on MVC. You can access it in NuGet `Install-Package MvcDonutCaching`. DevTrends also has a much more indepth article on the matter [here](http://www.devtrends.co.uk/blog/donut-output-caching-in-asp.net-mvc-3).

Because there's already a great article on output caching in MVC already. I'll focus on internationalization.

There are a couple unfortunate things about DevTrends MvcDonutCaching library 1) It is currently up for adoption and 2) It doesn't seem to currently have support for the VaryByHeader functionality in Microsoft's MVC OutputCaching.

###OutputCaching: Utilizing VaryByHeader
The OutputCache class has a `VaryByHeader` property that you can set to allow output cache keys to vary by headers passed from a browser. This is especially useful when your site is translated based on browser culture. The standard browser will send culture information up on a request in the `Accept-Language` header key. This header's value is a prioritized list of culture strings. For instance, if my main language is French, but I also understand English, my header might look like this from Firefox:

![firefox request headers]({{site.url}}/images/IRb2U83DK2m73PsgPRx-YuU2rlP2fb2RZokh8LfZ4NY.png)

You can specify that cache keys take this into consideration and append the header values to the keys so that visits in China don't influence the output of visitors in France. Below is an example of doing this in the attribute:

```csharp
[OutputCache(CacheProfile = "Cache1HourInternational", VaryByHeader = "Accept-Language")]
public ActionResult Index()
{
	return View();
}
```

By naming the CacheProfile, you also have the benefit of specifying in the config like so:

```xml
<caching>
      <outputCache defaultProvider="Memcached">
        <providers>
          <add name="Memcached" type="MemcachedOutputCacheProviderNamespace" />
        </providers>
      </outputCache>
      <outputCacheSettings>
        <outputCacheProfiles>
          <add name="Cache1HourInternational" duration="3600" varyByParam="none" varyByHeader="Accept-Language"/>
        </outputCacheProfiles>
      </outputCacheSettings>
    </caching>
```

With this, we can reliably output cache all pages from ActionResults that have the `OutputCache` attribute and the CacheProfile `Cache1HourInternational`.