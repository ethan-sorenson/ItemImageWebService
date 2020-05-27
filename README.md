# Item Images Web Service
 Import/Export BC Item Pictures
 
This service will help workaround the limitation in the Business Central web services that limits compatibility of web services and BLOBS.

I have a full blog that goes into more detail about the procedures used and how to consume the web service [here](https://www.eonesolutions.com/tech-tuesday-business-central-item-image-web-service/ "here").

### Overview
I had the requirement to import an Item Image into Business Central, but found it took more effort than I initially realized. 
Before we can begin, we need to understand how Business Central stores media. The actual file is stored in a binary large object ([BLOB](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/blob/blob-data-type "BLOB")) field. This field is stored in the Tenant Media table in Business Central. The [Media](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/media/media-data-type "Media") record is then included in a [Media Set](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/mediaset/mediaset-data-type "Media Set") on the Item record. This will allow multiple media objects to be linked to a single record. To keep this example simple, we will only work with a single image for each item, but the data structure looks like this:
![increment](https://i.imgur.com/C44tuKC.png)

### Getting Started
1. If you aren't familar with building AL extensions you can use the Microsoft [documentation](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-dev-overview "documentation") to get started.
2. The [Pag.83000.ItemBlobWs.al](Pag.83000.ItemBlobWs.al) file can be modified as needed to use additional logic.
3. If using this service to import Images, note that an existing images will be deleted prior to importing the new one.

### Troubleshooting
**Web Service isn't available after publishing**
* Make sure the service is published as outlined [here](https://docs.microsoft.com/en-us/dynamics365/business-central/across-how-publish-web-service "documentation").
* Make sure the service is named as expected ex. /ODataV4/Company('Sample')/ItemPictureWS

**Failed to create record.: The request was blocked by the runtime to prevent accidental use of production services.**
* Go to Business Central > Extensions > Item Image Web Service > Configure and enable ‘Allow HttpClient Requests’.

![increment](https://i.imgur.com/7echm3y.png)

**Web Service performance is slow**
* Due to the nature of all the file encoding and retrieval this is a slow web service compared to the standard ones.
* If you have any suggestions on how to improve the performance of this service feel free to open an issue.

**Something else isn't working properly**
* Use github's issue reporter on the right
* Send me an email ethan.sorenson@eonesolutions.com (might take a few days)

### Updates
* 1.0.0.0 first release on BC v16

***Enjoy!***

