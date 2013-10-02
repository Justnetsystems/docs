This module adds admin functionality to manage search facets and search redirects through the admin. While the domain is available
as apart of our community offering in the framework itself, this admin module provides easier ways to administer this information in
the database.

Screenshots of the admin capabilities:

[![Facet Management](modules/AdvancedSearchAdmin-Facets.png)](_img/modules/AdvancedSearchAdmin-Facets.png)
[![Search Redirect Management](modules/AdvancedSearchAdmin-Redirect.png)](_img/modules/AdvancedSearchAdmin-Redirect.png)
[![Category Facet Management](modules/AdvancedSearchAdmin-CategoryFacets.png)](_img/modules/AdvancedSearchAdmin-CategoryFacets.png)

To include this in your project, simply follow the steps below (up-to-date diff from DemoSite)[https://github.com/broadleafcommerce/demosite/compare/develop...advanced-search]

1. Add the required dependency management to the parent pom

    ```xml
    <dependency>
        <groupId>com.broadleafcommerce</groupId>
        <artifactId>broadleaf-admin-search</artifactId>
        <version>1.0.0-SNAPSHOT</version>
        <type>jar</type>
        <scope>compile</scope>
    </dependency>
    ```

2. Add the required dependency to the admin pom

    ```xml
    <dependency>
        <groupId>com.broadleafcommerce</groupId>
        <artifactId>broadleaf-admin-search</artifactId>
    </dependency>
    ```

3. Add the following line to your .gwt.xml file

    ```xml
    <inherits name="com.broadleafcommerce.search.admin.searchModule" />
    ```

4. Add the necessary module keys in the database

    ```sql
    INSERT INTO BLC_ADMIN_SECTION (ADMIN_SECTION_ID, ADMIN_MODULE_ID, NAME, SECTION_KEY, URL, USE_DEFAULT_HANDLER) VALUES (20, 1, 'Search Facet', 'SearchFacet', '/search-facet', TRUE);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (20,6);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (20,7);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (20,8);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (20,9);
    INSERT INTO BLC_ADMIN_SECTION (ADMIN_SECTION_ID, ADMIN_MODULE_ID, NAME, SECTION_KEY, URL, USE_DEFAULT_HANDLER) VALUES (21, 1, 'Search Redirect', 'SearchRedirect', '/search-redirect', TRUE);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (21,6);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (21,7);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (21,8);
    INSERT INTO BLC_ADMIN_SECTION_PERMISSION_XREF (ADMIN_SECTION_ID, ADMIN_PERMISSION_ID) VALUES (21,9);
    ```

5. If you based your implementation on the heatclinic demo, then you should already have the file messages-admin.properties.
You will need to add the following lines to account for the new admin sections:

    ```
    BLCMerchandising.SearchFacet=Search Facet
    BLCMerchandising.SearchRedirect=Search Redirect
    ```

Also, make sure support for messages-admin is included in your app. Check for the following in your app context xml
and add if it's not there. Note - this generally appears in the file /WEB-INF/applicationContext-admin.xml.

    ```xml
    <bean id="resourceBundleExtensionPoint" class="org.broadleafcommerce.common.util.ResourceBundleExtensionPoint" />
    <bean id="messageSource"
          class="org.broadleafcommerce.common.util.BLResourceBundleMessageSource">
        <constructor-arg>
            <list>
                <value>messages-admin</value>
            </list>
        </constructor-arg>
        <constructor-arg ref="resourceBundleExtensionPoint" />
    </bean>
    ```
