# Trackingplan GTM Template

A Google Tag Manager custom template to install and configure [Trackingplan](https://www.trackingplan.com/) on your website in a cleaner and more manageable way.

This template helps you initialize Trackingplan from GTM and configure the main web tracking options without having to maintain a Custom HTML tag manually.

## What this template does

This template loads the Trackingplan script and initializes it using your Trackingplan ID.

It also allows you to configure optional web implementation settings from the GTM interface, including:

- Environment
- Source alias
- Debug mode
- Privacy encryption control
- Tags / custom parameters
- Custom monitored domains
- Custom data layer getter

The template only sends optional configuration values when they are explicitly set in the interface.

## Recommended setup

Trackingplan should usually be loaded as early as possible in the page lifecycle so it can monitor web requests and browser-side analytics activity from the beginning.

Recommended GTM setup:

- **Tag type:** Trackingplan custom template
- **Trigger:** Initialization - All Pages
- **Tag firing options:** Once per page
- **Priority:** High, if you need Trackingplan to run before other tags

## Configuration fields

### Trackingplan ID

Your Trackingplan ID.

This field is required to initialize Trackingplan.

### Environment

Allows you to isolate data between production and testing environments.

Available values:

- `PRODUCTION`
- `DEV`

Recommended use:

- Use `PRODUCTION` for your live website.
- Use `DEV` for staging, QA, testing, or development environments.

### Source alias

Optional.

Allows you to differentiate between website sources or implementations.

Example: `"nosDeuWEB"`

Leave it empty unless you need to identify a specific website, market, subdomain, implementation, or web data stream inside Trackingplan.

### Debug mode

Optional.

Controls whether Trackingplan debugging information is shown in the browser console.

Available values:

- `false`
- `true`

Recommended use:

- Keep it as `false` for production.
- Use `true` only while testing or debugging the implementation.

### Privacy encryption

Optional.

Leave as **Do not set** unless you need to explicitly control Trackingplan privacy encryption for detected personal data.

When enabled, Trackingplan encrypts detected personal data in its privacy report.

If left as **Do not set**, the template does not send the `usePrivacy` option and Trackingplan will use its default behavior.

### Tags / custom parameters

Optional.

Tags allow you to add custom metadata to the data sent to Trackingplan.

They can be useful to distinguish warnings, segment event traffic, debug implementations, or identify releases and test variants.

Example:

{
  "country": "es",
  "market": "spain",
  "pageType": "product",
  "release": "v1.2.0"
}

Common web use cases:

- Country
- Market
- Release version
- Page type
- Site section
- Template type
- Brand
- Business unit

### Custom domains

Optional.

Use this option when your analytics, marketing, consent, personalization, or tracking requests are sent to domains that Trackingplan should also monitor.

The format is:

{
  "myAnalyticsDomain.com": "My analytics alias"
}

Example:

{
  "posthog.com": "Posthog"
}

This means that requests made to `posthog.com` will also be forwarded to Trackingplan and identified with the alias `Posthog`.

This can be useful when your website sends tracking hits to custom collection domains, third-party analytics endpoints, server-side tagging endpoints, or vendor domains that are not covered by the default setup.

Use this field only when you need Trackingplan to monitor additional request domains.

### getDataLayer

Optional and advanced.

Allows you to provide a custom function to return your website data layer.

This can be useful when your website data layer is not named `dataLayer`.

Example:

function() {
  return window.customDataLayer;
}

In GTM, the recommended approach is to use a Custom JavaScript Variable that returns the expected data layer reference or function, instead of pasting complex logic directly into the template field.

## Example initialization

The template builds a configuration object and initializes Trackingplan using:

Trackingplan.init(TRACKINGPLAN_ID, config);

Only the options configured in the GTM interface are added to `config`.

Example output:

Trackingplan.init("YOUR_TRACKINGPLAN_ID", {
  environment: "PRODUCTION",
  sourceAlias: "TrackingplanWEB",
  debug: false,
  tags: {
    country: "es",
    market: "spain",
    pageType: "product"
  }
});

## Permissions

This template may require permissions to:

- Inject the Trackingplan script.
- Access GTM-provided template data.
- Read optional configuration values.
- Use optional custom JavaScript values depending on your setup.

Review the template permissions carefully before publishing it in your GTM container.

## Notes

This is not an official Trackingplan template unless explicitly stated by Trackingplan.

It is a community/custom GTM template created to make Trackingplan web implementation easier, cleaner, and more maintainable from Google Tag Manager.

## Useful links

- [Trackingplan documentation](https://www.trackingplan.com/docs/installing-trackingplan/installing-trackingplan-on-your-websites?utm_source=google_tag_manager&utm_medium=template&utm_campaign=trackingplan_gtm_template&utm_content=trackingplan_documentation)
- [nosDeu - The Data Cooperative 🐮](https://nosdeu.com/?utm_source=google_tag_manager&utm_medium=template&utm_campaign=trackingplan_gtm_template&utm_content=nosdeu_information)

## Support

If you have any questions, you can send me a message on [LinkedIn](https://www.linkedin.com/in/braiscalvo/) or contact us through [nosDeu](https://nosdeu.com/).