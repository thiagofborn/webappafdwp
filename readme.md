# Azure Web App hosting Wordpress with Azure Front Door

First of all, it was a migration from a Wordpress vanilla host.

Some steps used to host a Wordpress app on an Azure Web App.
Setup description will be detailed in the future(or not).

In short:

1. Azure Web App - Networked rule closing access
2. Azure MySQL DB - SSL enforced
3. Azure Front Door - Used for cache and to associated with a WAF
4. Update internal links via SQL

## Update internal links via SQL UPDATE

The links where build pointing directly to the "https://wastelandweb.azurewebsites.net", and this link is from the Azure Web App. I would like to set up the links correctly to point to my custom domain. The custom domain is defined at my Azure Front Door service, and it has WAF enabled.

For that, I will need to update the links inside the MySQL DB. One way to do that is:

Example:

```sql
UPDATE wp_posts SET post_content=REPLACE (post_content, "wastelandweb.azurewebsites.net/blog", "www.wastelandweb.com/blog")
```

## References

Some references and tests. What helped and what did not.

1. Multisite - <https://github.com/uglide/azure-content/blob/master/articles/app-service-web/web-sites-php-convert-wordpress-multisite.md>
2. Web site used for tests - <https://www.wastelandweb.com>

## Deploy this solution

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)