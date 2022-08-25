# 🚀 Booth Centre Protoype Strapi API

This is the prototype backend for the booth centre CMS. 

## Content types and structure
The API is built with the following collection types. These are schemas for data that is repeated such as artworks:

### Artist
| Field Name   | Type                | Required | Description                            |
| ------------ | ------------------- |  :-----: | -------------------------------------- |
| name         | String              | &check;  | The artists real name. Needed for booth centre staff to identify the artist |
| anonymous    | Boolean             | &check;  | If selected, artists work will appear on site, but pseudonym will be used in place of their real name |
| pseudonym    | String              |          | The artists chosen pseudonym. Required if `anonymous` is selected (must also be a unique value) |
| hide         | Boolean             | &check;  | If selected, artist will not be shown on site |
| introduction | String              |          | A description of the artist themselves |
| passphrase   | String              | &check;  | A short phrase chosen by the artist to authenticate themselves to booth cantre staff |
| artworks     | Relation to artwork |          | All artworks associated with the artist. Selected using dropdown in interface |


### Artwork
| Field Name   | Type                | Required | Description                            |
| ------------ | ------------------- |  :-----: | -------------------------------------- |
| title        | String              | &check;  | The artists real name. Needed for booth centre staff to identify the artist |
| description  | String              | &check;  | A short description of the piece of artwork |
| medium       | Enumeration         | &check;  | One of the given values of `Drama performance`, `Painting`, `Poem`, `Sculpture` or `Story` |
| hide         | Boolean             | &check;  | If selected, artwork will not be shown on site |
| artist       | Relation to artist  |          | Artist who completed the work. Selected using dropdown in interface |
| textContent  | String              |          | The work itself (if text based) |
| mediaContent | String              |          | The work itself, if a non text based format |


### Collection
| Field Name   | Type                 | Required | Description                            |
| ------------ | -------------------- |  :-----: | -------------------------------------- |
| title        | String               | &check;  | The title of the collection of pieces of art |
| description  | String               | &check;  | A description of the collection |
| hide         | Boolean              | &check;  | If selected, the collection will not be shown on site |
| artworks     | Relation to artworks |          | All artworks associated with the artist. Selected using dropdown in interface |

While Strapi is very flexible and easy to use, there are a few issues with data that must be handled:
#### Relational fields for data entities cannot be marked as required
While most fields can be marked as required to prevent submission with empty values, relation fields do not allow this. They also do not allow for a default value to be given if nothing is chosen. This means that if a user does not provide a value for a relational field it will be provided to the calling application as null. This must be handled by the consuming app to prevent unwanted behaviour

#### Storing of images and non text type files
In the production environment, the application will be on a server with storage for all image files in the default `/uploads` directory provided by Strapi. This will behave in the same way as the local environment in terms of the file paths, to verify what is being stored in this database open `./tmp/data.db` in a database tool such as TablePlus


### Single types
Single types are used for fields that need to be editable, but are uniform throughout. To save on multiple API calls, a single collection type has been created for all static page content:

### StaticPageContent
| Field Name                   | Type      | Required | Description                            |
| ---------------------------- | --------- |  :-----: | -------------------------------------- |
| CollectionsPageTitle         | String    | &check;  | The text at the top of the collections page |
| CollectionsPageIntroduction  | String    |          |  The introduction text for the collections page |
| ArtistsPageTitle             | String    | &check;  | The text at the top of the artists page |
| ArtistsPageIntroduction      | String    |          |  The introduction text for the artists page |
| ArtworksPageTitle            | String    | &check;  | The text at the top of the artworks page |
| ArtworksPageIntroduction     | String    |          |  The introduction text for the artworks page |

## Setup
- The project must be run locally. Running `npm i` will install the project, create all the needed tables and will populate the interface (accessible at localhost:1337/admin), but will not provide any data.
- A `.env` file must be created in the same format as `.env.example`

### Node version
You  must have node version ^16.0.0 installed locally to run the project. Run `node --version` to check your currently used version, and if required a node version version such as [nvm](https://github.com/nvm-sh/nvm) or [n](https://github.com/tj/n) can be used to install it.

## Strapi info
Strapi comes with a full featured [Command Line Interface](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html) (CLI) which lets you scaffold and manage your project in seconds.

### `develop`

Start your Strapi application with autoReload enabled. This will allow you to make changes to the API in the content-type builder [Learn more](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html#strapi-develop)

```
npm run develop
```

### `start`

Start your Strapi application with autoReload disabled. In this mode, you will not be able to make changes to the content type builder, if this is the aim use `npm develop`. [Learn more](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html#strapi-start)

```
npm run start
```

### `build`

Build your admin panel. [Learn more](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html#strapi-build)

```
npm run build
```

## ⚙️ Deployment

Strapi gives you many possible deployment options for your project. Find the one that suits you on the [deployment section of the documentation](https://docs.strapi.io/developer-docs/latest/setup-deployment-guides/deployment.html).

## 📚 Learn more

- [Resource center](https://strapi.io/resource-center) - Strapi resource center.
- [Strapi documentation](https://docs.strapi.io) - Official Strapi documentation.
- [Strapi tutorials](https://strapi.io/tutorials) - List of tutorials made by the core team and the community.
- [Strapi blog](https://docs.strapi.io) - Official Strapi blog containing articles made by the Strapi team and the community.
- [Changelog](https://strapi.io/changelog) - Find out about the Strapi product updates, new features and general improvements.

Feel free to check out the [Strapi GitHub repository](https://github.com/strapi/strapi). Your feedback and contributions are welcome!

## ✨ Community

- [Discord](https://discord.strapi.io) - Come chat with the Strapi community including the core team.
- [Forum](https://forum.strapi.io/) - Place to discuss, ask questions and find answers, show your Strapi project and get feedback or just talk with other Community members.
- [Awesome Strapi](https://github.com/strapi/awesome-strapi) - A curated list of awesome things related to Strapi.
