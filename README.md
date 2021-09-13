# How to Build a Storefront with Gatsby.js and Shopify (storyblok-shopify-gatsby repo)

This is a hands-on tutorial to build Storyblok with Gatsby & Shopify e-commerce project.

Before reading this tutorial, make sure to complete these steps first in a listed order.

1. [Storyblok: Storefront Setup](https://www.storyblok.com/docs/guide/integrations/ecommerce/storefront-setup)
2. [Storyblok: Shopify](https://www.storyblok.com/docs/guide/integrations/ecommerce/shopify)
3. [Storyblok: eCommerce Field-Type Plugin](https://www.storyblok.com/docs/guide/integrations/ecommerce/integration-plugin)

> 💡 Notes: You'll need to apply for getting access for eCommerce integration in Storyblok. 👉 [https://www.storyblok.com/fs/enterprise-contact](https://www.storyblok.com/fs/enterprise-contact)

# Environment setup

- Install `gatsby-cli`

```
$ npm install -g gatsby-cli
```

- Create e-commerce starter with `gatsby-shopify-starter`

> [Gatsby: gatsby-starter-shopify](https://www.gatsbyjs.com/starters/gatsbyjs/gatsby-starter-shopify)

```
$ gatsby new gatsby-starter-shopify https://github.com/gatsbyjs/gatsby-starter-shopify
$ cd gatsby-starter-shopify
$ gatsby develop
```

5. Check `localhost:8000`. You can see gatsby-shopify-starter is running in the browser.

# Connect Storyblok

- Login to Storyblok
- Install `gatsby-source-storyblok` to link Storyblok and GraphQL
- Install `@storyblok/storyblok-editable` for editor interface
- Install `storyblok-js-client`
```
$ npm install --save gatsby-source-storyblok @storyblok/storyblok-editable storyblok-js-client
```

- Settings -> General Tab -> Fill **"Location (default environment)"** as **"http://localhost:8000/"**
- Settings -> General Tab -> Fill **"Preview urls"** as **"dev"** and **"http://localhost:8000"**
- Settings -> API-Keys -> Copy the preview token

![settings](./images/settings.png)

- Paste the preview token into `.env.development` & `.env.production`

 `.env.development` & `.env.production`

```
GATSBY_STOREFRONT_ACCESS_TOKEN=YOUR_STORE_ACCESS_TOKEN
GATSBY_SHOPIFY_STORE_URL=your-shop.myshopify.com
SHOPIFY_ADMIN_PASSWORD=YOUR_SHOPIFY_ADMIN_PASSWORD
```

You can find the domain name of your Shopify shop name & storefront API from this step we completed.

> [Storyblok: Shopify](https://www.storyblok.com/docs/guide/integrations/ecommerce/shopify)

> Admin password can be found in `Apps → manage private apps → Admin API → Password`

- Configure the preview token from `.env.development` & `.env.production` files into `gatsby-config.js` file

 `gatsby-congif.js`

```javascript
module.exports = {
  siteMetadata: {
    title: 'Gatsby Default Starter',
  },
  plugins: [
    {
      resolve: "gatsby-source-shopify",
      options: {
        password: process.env.SHOPIFY_ADMIN_PASSWORD,
        storeUrl: process.env.GATSBY_SHOPIFY_STORE_URL,
        shopifyConnections: ["collections"],
      },
    },
    {
      resolve: 'gatsby-source-storyblok',
      options: {
        accessToken: process.env.STORYBLOK_TOKEN,
        homeSlug: 'home',
        version: process.env.NODE_ENV === 'production' ? 'published' : 'draft'
      }
    },
    ...
  ]
}
```

For more environment variables, you can check Gatsby's documentation.

> [Gatsby: Environment Variables](https://www.gatsbyjs.com/docs/how-to/local-development/environment-variables/)

- Start the server to check everything works

```
$ gatsby develop
```

# Notes

- Start from "eCommerce Field-Type Plugin"
- After that, starting from "eCommerce Integration" in ["How to Build a Storefront with Next.js and BigCommerce"](https://www.storyblok.com/tp/storefront-next-bigcommerce)