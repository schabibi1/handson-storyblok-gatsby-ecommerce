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

> [Gatsby: gatsby-shopify-starter](https://www.gatsbyjs.com/starters/AlexanderProd/gatsby-shopify-starter)

```
$ gatsby new gatsby-shopify-starter https://github.com/AlexanderProd/gatsby-shopify-starter
$ cd gatsby-shopify-starter
$ gatsby develop
```

5. Check `localhost:8000`. You can see gatsby-shopify-starter is running in the browser.

# Connect Storyblok

- Login to Storyblok
- Install `gatsby-source-plugin` to link Storyblok and GraphQL & Install `storyblok-react` for editor interface

```
$ npm install --save gatsby-source-storyblok storyblok-react
```

- Settings -> General Tab -> Fill **"Location (default environment)"** as **"http://localhost:8000/"**
- Settings -> General Tab -> Fill **"Preview urls"** as **"dev"** and **"http://localhost:8000"**
- Settings -> API-Keys -> Copy the preview token

![settings](./images/settings.png)

- Paste the preview token into `.env.development` & `.env.production`

 `.env.development` & `.env.production`

```
SHOP_NAME=DOMAIN_NAME_OF_YOUR_SHOPIFY_SHOP_NAME
SHOPIFY_ACCESS_TOKEN=YOUR_STOREFRONT_API
STORYBLOK_TOKEN=YOUR_PREVIEW_TOKEN
```

You can find the domain name of your Shopify shop name & storefront API from this step we completed.

> [Storyblok: Shopify](https://www.storyblok.com/docs/guide/integrations/ecommerce/shopify)

- Configure the preview token from `.env.development` & `.env.production` files into `gatsby-config.js` file

 `gatsby-congif.js`

```javascript
module.exports = {
  siteMetadata: {
    title: 'Gatsby Default Starter',
  },
  plugins: [
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

- Start the servert to check everything works

```
$ gatsby develop
```

# Notes

- Start from "eCommerce Field-Type Plugin"