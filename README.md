# What is it?
Unsplash is a .NET Core 3.1 library for getting freely usable photos from the Unsplash web service. 

The library gives you free access to a vast array of freely distributable photos and photo collections. 
It lets you list, seearch through and download via an easy to use, clean API.

The UnsplashLibrary is distributed as a NuGet package for easy integration into .NET projects of various kinds.

# How do I use it?
First you have to install it into your project by one of the following ways:

- **Package Manager Console**: `Install-Package UnsplashClient -Version 2.0.1`
- **.NET CLI**: `dotnet add package UnsplashClient --version 2.0.1`
- **PackageReference** in your project config: `<PackageReference Include="UnsplashClient" Version="2.0.1" />`.

Then, make a new instance of the [Unsplash.Client](#Client) class and call any of its public methods methods 
to get data.

Here's a list of [Unsplash.Client](#Client)'s public API:

<span id="public-api"></span>
## Working with photos:
- ListPhotosAsync([ListPhotosRequest](#ListPhotosRequest)? request = null)
  - Get a list of [Photo](#Photo) objects asynchronously.
  - **Arguments:** A [ListPhotosRequest](#ListPhotosRequest) object with 
    parameters for the request (optional). 
    If left at `null`, [default parameters](#default-parameters) are used.
  - **Returns:** A `List<Photo>` object.
  
- GetPhotoAsync(string id)
  - Get data for a single photo asynchronously.
  - **Arguments:** The `id` of the photo you want to get data for. 
    Typically you get photo ids from method that return [Photo](#Photo) or `List<Photo>`.
  - **Returns:** A [Photo](#Photo) object.
  
- GetRandomPhotoAsync([GetRandomPhotoRequest](#GetRandomPhotoRequest)? request = null)
  - Get a random photo asynchronously.
  - **Arguments:** A [GetRandomPhotoRequest](#GetRandomPhotoRequest) object with 
    parameters for the request (optional).
    If left at `null`, [default parameters](#default-parameters) are used.
  - **Returns:** A [Photo](#Photo) object.
  
- GetRandomPhotosAsync(uint count)
  - Get a list of random photos asynchronously.
  - **Arguments:** A `count` that signifies the number of photos to get.
  - **Returns:** A `List<Photo>` object.
  
- GetRandomPhotosAsync([GetRandomPhotosRequest](#GetRandomPhotosRequest)? request = null)
  - Get a list of random photos asynchronously.
  - **Arguments:** A [GetRandomPhotosRequest](#GetRandomPhotosRequest) object with 
    parameters for the request (optional).
    If left at `null`, [default parameters](#default-parameters) are used.
  - **Returns:** A `List<Photo>` object.
  
- GetPhotoStatsAsync(string id)
  - Get photo [Stats](#Stats) asynchronously.
  - **Arguments:** The `id` of the photo you want to get stats for. 
    Typically you get photo ids from method that return [Photo](#Photo) or `List<Photo>`.
  - **Returns:** A [Stats](#Stats) object.
  
- GetPhotoStatsAsync(GetPhotoStatsRequest request)
  - Get photo [Stats](#Stats) asynchronously.
  - **Arguments:** A [GetPhotoStatsRequest](#GetPhotoStatsRequest) object with 
    parameters for the request.
  - **Returns:** A [Stats](#Stats) object.
  
- SearchPhotosAsync(string query)
  - Search for photos asynchronously.
  - **Arguments:** A search term to find photos by.
  - **Returns:** A [Photos.SearchResults](#Photos-SearchResults) object.
  
- SearchPhotosAsync([SearchPhotosRequest](#SearchPhotosRequest) request)
  - Search for photos asynchronously.
  - **Arguments:** A [SearchPhotosRequest](#SearchPhotosRequest) object with 
    parameters for the request.
  - **Returns:** A [Photos.SearchResults](#Photos-SearchResults) object.
  - **Throws:** An `ArgumentNullException` if `request` is null.
  
- DownloadPhotoAsync(Uri url, string id, string destination)
  - Download a photo asynchronously.
  - **Arguments:** A `url` of the photo, its `id` used to mark the photo as downloaded 
    (Unsplash policy) and the file system `destination` of the downloaded file. 
  - **Returns:** The length in bytes of the downloaded file.
  
- DownloadPhotoAsync([DownloadPhotoRequest](#DownloadPhotoRequest) request, string id, 
  string destination)
  - Download a photo asynchronously.
  - **Arguments:** A [DownloadPhotoRequest](#DownloadPhotoRequest) object with 
    parameters for the request, the photo's `id` used to mark the photo as downloaded 
    (Unsplash policy) and the file system `destination` of the downloaded file. 
  - **Returns:** The length in bytes of the downloaded file.
  - **Throws:** An `ArgumentNullException` if `request` is null.
  
  
## Working with photo collections
- SearchCollectionsAsync(string query)
  - Search for collections asynchronously.
  - **Arguments:** A search term to find collections by.
  - **Returns:** A [Collections.SearchResults](#Collections-SearchResults) object.
  
- SearchCollectionsAsync([SearchCollectionsRequest](#SearchCollectionsRequest) request)
  - Search for collections asynchronously.
  - **Arguments:** A [SearchCollectionsRequest](#SearchCollectionsRequest) object with 
    parameters for the request
  - **Returns:** A [Collections.SearchResults](#Collections-SearchResults) object.
  - **Throws:** An `ArgumentNullException` if `request` is null.
  
- ListFeaturedCollectionsAsync([ListFeaturedCollectionsRequest](#ListFeaturedCollectionsRequest) request)
  - List featured collections asynchronously.
  - **Arguments:** A [ListFeaturedCollectionsRequest](#ListFeaturedCollectionsRequest) object with 
    parameters for the request (optional).
  - **Returns:** A `List<Collection>` object.
  
- GetCollectionAsync(string id)
  - Get data for a single [Collection](#Collection) asynchronously.
  - **Arguments:** The `id` of the collection to get data for.
  - **Returns:** A [Collection](#Collection) object.
  
- GetCollectionPhotosAsync(string id)
  - Get a list of [Photo](#Photo)s in a [Collection](#Collection) asynchronously.
  - **Arguments:** The `id` of the collection to get the photos of.
  - **Returns:** A `List<Photo>` object.
  
- ListRelatedCollectionsAsync(string id)
  - Get a list of collections related to a [Collection](#Collection), asynchronously.
  - **Arguments:** The `id` of the collection to get related collections of.
  - **Returns:** A `List<Collection>` object.
  
  

<span id="Photos-SearchResults"></span>
### Unspslash.Photos.SearchResults
A class that contains the results of a photo search. It has three public properties:

- List<Photo> **results** - a list of search matches
- uint **total** - a number of total matches matches
- uint **total_pages** - a number of results pages

<span id="Collections-SearchResults"></span>
### Unspslash.Collections.SearchResults
A class that contains the results of a collection search. It has three public properties:

- **results** - a `List<Collection>` with search matches
- **total** - a number of total matches matches
- **total_pages** - a number of results pages
  
## Request types
<span id="ListPhotosRequest"></span>
### Unsplash.Requests.ListPhotosRequest
Sets parameters for a request to list photos.
The class accepts three arguments in its constructor:
- [Order](#Order) **order** - the ordering to apply to photos
- uint **page** - the page to show
- uint **perPage** - the number of photos to show per page


<span id="GetRandomPhotoRequest"></span>
<span id="GetPhotoStatsRequest"></span>


### The Unsplash.Client class
<span id="Client"></span>
The **Unsplash.Client** class is the main gateway into the system. In order to use its [APIs](#public-api) 
you instantiate it with an Unsplash API access key which you can obtain from 
[Unsplash Developer](https://unsplash.com/oauth/applications).

### Default parameters
<span id="default-parameters"></span>