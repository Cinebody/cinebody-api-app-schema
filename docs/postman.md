[Cinebody](https://www.cinebody.com) is the video production platform for every organization.

Check out the platform with a [Free Trial](https://pro.cinebody.com/checkout/trial)

If you have needs that require API access, **get in touch about our [Enterprise Plans](https://www.cinebody.com/enterprise-scheduling)** or email [support@cinebody.com](mailto:support@cinebody.com).

# API Status

See the latest api status: [https://status.cinebody.com/](https://status.cinebody.com/)

# Requirements

To get started you'll need an **API Key**.

# Security

**Never share your API Key or expose it publicly!** Your key should only be used to make requests from server-side environments. You should never use the API Key from a frontend application.

# Authentication

Every request you make should include the `x-api-key` header where the value is your api key.

# Nomenclature

* API App
  * An app that accesses the Cinebody API using an API Key. **This documentation is for API Apps.**
* Organization
  * An organization has many teams. Think of an organization like company where the teams are different divisions.
* Team
  * A team has many projects.
* Project
  * A project is like a campaign with a start and end. Creators join your project and upload footage. Your team admins then review that content
* User [aka Creator]
  * A user might belong to many organizations, teams, and/or projects with various roles
* MediaFile [aka Video or Clip]
  * Clip
    * A clip is a video that is uploaded to a project
  * Final Video
    * A final video is an edited video that team admins may upload to a project and then optionally share to Creators
* Notification
  * A notification can be sent to Creators on a team or project. Notifications will show in the Cinebody App and as a push notification [if enabled by the user]

# User Roles

Users can have various roles within different organizations, teams, or projects.

* Organization Admin
  * Can manage organization branding, payment information, etc.
  * Has admin permissions in all Teams under the organization
* Team Admin
  * Can add additional team admins
  * Can moderate content within team projects
* Project Creator
  * Has joined a project either via invite or join code
  * Can upload clips through the Cinebody App or manually through pro.cinebody.com

# Rate Limits / Throttling

We employ rate limiting of api requests but do not publish specific limits. If you're encountering rate limiting issues and need higher limits please contact us at [support@cinebody.com][support@cinebody.com]

# Errors

Error responses from the api will have:

* `status` - Will always be 'failure'
* `code` - An error code in UPPER_SNAKE_CASE. Use this code to check for specific errors.
* `reason` - A debug message meant for developers
* `friendlyReason` - An end-user friendly error message that can be displayed

For example:

```
{
	status: 'failure',
	code: 'CODE_TAKEN',
	reason: 'The code is already taken.  Use a different code.',
	friendlyReason: 'Sorry, that code is already taken. Try a different code.'
}
```

## HTTP Codes

* `200` - Success
* `400` - Bad request. Generally this is poorly formatted data. Check your parameters and read the `code` and `reason` in the error response.
* `403` - Not Authorized. Check the organization/team/etc, that your app has access to it, and that you've properly set your api key.
* `404` - The item that was requested couldn't be found.
* `406` - Generally missing or invalid parameters
* `410` - Deprecated endpoint
* `418` - [I'm a teapot](https://datatracker.ietf.org/doc/html/rfc2324#section-2.3.2)
* `420/429` - You've been rate-limited. Enhance your calm
* `500` - Catch-all error. Check the format of your parameters / request.

# Optimization

Many endpoints allow you to specify `attributes` to limit the response to only data you need. You can use this to reduce the over-the-wire size of response data.
