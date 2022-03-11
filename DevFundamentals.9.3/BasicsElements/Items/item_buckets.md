## Item buckets

[docu](https://doc.sitecore.com/xp/en/users/101/sitecore-experience-platform/using-item-buckets.html)

Item buckets let you manage large numbers of items in the content tree. 

An item bucket is a container that you can use to hide a large number of items and still easily retrieve and work with these items.

The only way to find bucket items is to use the Sitecore search engine.

Items relationships are removed, and items are organized in a folder structure according to the date and time they were created. It stores items that don't need a hierarchy.

It improves performance.

Item bucket can contain:

- **regular items** which are visible in the content tree. These items are based on templates that does not support item buckets.

- **bucketable items** unstructure items that are hidden in the content tree and they don't mantain any relationship.

`do not store both items in an item bucket. This can cause errors`

Whenever you change the bucketable settings for items in an items bucket, you must synchronize the item bucket.

### View hidden items

- click the item-bucket
- Search tab in the **editing panel**

- In the ribbon click the view tab.
- In the view group, select the buckets check box