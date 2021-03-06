<template>
  <div>
    <Page :title="title" :side="side" :crumbs="crumbs" no-hero no-head>
      <h1 class="mb-4">Lookup API</h1>

      <p>
        Perform near-instant technology lookups with the Lookup API. Results are
        fetched from our comprehensive database of millions of websites. If we
        haven't seen a domain before, we'll index it immediately and report back
        within minutes.
      </p>

      <p>
        Results are site-wide and may even include pages behind logins that
        typical crawlers can't reach. Where available, country, language and
        traffic data are included.
      </p>

      <Heading id="endpoint" size="2" class="mt-8 mb-4"> Endpoint </Heading>

      <p><code>GET</code> <code>https://api.wappalyzer.com/lookup/v2/</code></p>

      <Heading id="properties" size="2" class="mt-8 mb-4"> Properties </Heading>

      <v-card class="my-4" flat outlined>
        <v-simple-table>
          <thead>
            <tr>
              <th width="30%">Property</th>
              <th>Description</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Execution</td>
              <td>
                Synchronous / Asynchronous (when response yields no results)
              </td>
            </tr>
            <tr>
              <td>Request timeout</td>
              <td>30s</td>
            </tr>
            <tr>
              <td>Rate limit</td>
              <td>1 request / second (up to ten domains per request)</td>
            </tr>
          </tbody>
        </v-simple-table>
      </v-card>

      <Heading id="parameters" size="2" class="mt-8 mb-4"> Parameters </Heading>

      <v-card class="my-4" flat outlined>
        <v-simple-table>
          <thead>
            <tr>
              <th width="30%">Name</th>
              <th>Description</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <code>urls</code>&nbsp;<em class="text--disabled"
                  >(required)</em
                >
              </td>
              <td>
                Between one and ten website URLs, comma-separated (e.g.
                <code>https://example.com,https://example.org</code>).
              </td>
            </tr>
            <tr>
              <td><code>callback_url</code></td>
              <td>
                If instant results are unavailable, A POST request will be made
                to the callback URL upon completion of the request (e.g.
                <code>https://yourdomain.com</code>).
              </td>
            </tr>
            <tr>
              <td><code>denoise</code></td>
              <td>
                Exclude low confidence results (<code>true</code> (default) or
                <code>false</code>).
              </td>
            </tr>
            <tr>
              <td><code>max_age</code></td>
              <td>
                Return results of up to <code>max_age</code> months old
                (<code>1</code>-<code>12</code>). Set to <code>1</code> to only
                return fresh results. Defaults to <code>2</code>.
              </td>
            </tr>
            <tr>
              <td><code>squash</code></td>
              <td>
                Combine monthly results into a single set when
                <code>true</code> (default). Set to <code>false</code> to group
                results by month.
              </td>
            </tr>
            <tr>
              <td><code>sets</code></td>
              <td>
                Comma-separated list of additional field sets to include in the
                results (e.g. <code>meta,social</code>). See
                <nuxt-link to="/docs/fields/"> Fields </nuxt-link>. Use
                <code>all</code> to include all fields.
              </td>
            </tr>
          </tbody>
        </v-simple-table>
      </v-card>

      <Heading id="callback" size="2" class="mt-8 mb-4"> Callback </Heading>

      <p>
        A callback URL is a public endpoint hosted on your own server. If you
        request a domain that we haven't seen before, you'll initially get an
        empty response while the website is being indexed. Minutes later, your
        callback URL will receive a POST request with the final results. Without
        a callback URL, you will not get these results unless you make another
        request.
      </p>

      <v-alert
        :icon="mdiLightbulbOnOutline"
        color="secondary"
        class="my-8 elevation-1"
      >
        When a crawl is initiated, subsequent requests for the same URL are free
        for one hour. Allow for up to 15 minutes for the crawl to complete
        before re-trying a request. This allows you to get results without the
        need for a public callback endpoint.
      </v-alert>

      <v-alert
        :icon="mdiLightbulbOnOutline"
        color="secondary"
        class="my-8 elevation-1"
      >
        To verify that the request was made by Wappalyzer, enable
        <nuxt-link :to="{ path: '/docs/api/v2/basics', hash: 'signatures' }">
          callback signatures </nuxt-link
        >.
      </v-alert>

      <Heading id="examples" size="2" class="mt-8 mb-4"> Examples </Heading>

      <v-card class="mb-8">
        <v-card-title class="subtitle-2"> Example request </v-card-title>
        <v-card-text>
          <p>
            In this example we request two URLs with a callback URL and the
            default options.
          </p>

          <pre><Code>curl -H "x-api-key: &lt;your api key&gt;" "https://api.wappalyzer.com/lookup/v2/?urls=https://example.com,https://example.org&amp;callback_url=https://yourdomain.com"</Code></pre>
        </v-card-text>

        <v-divider />

        <v-card-title class="subtitle-2">
          Example response (success)
        </v-card-title>
        <v-card-text>
          <p>
            We get a result for each URL, in this case one successful and one
            empty. An empty response means the website has either not been
            indexed, or no technologies were found. The <code>crawl</code> field
            indicates that a crawl has been initiated. When ready, results will
            be sent to the callback URL provided.
          </p>

          <p>
            The <code>trafficRank</code> value is a relative traffic indicator.
            A higher number means a more trafficked website. A value of zero
            means traffic information is unavailable.
          </p>

          <pre><Code>[
  {
    "url": "https://example.com",
    "technologies": [
      {
        "slug": "craft-cms",
        "name": "Craft CMS",
        "categories": [
          {
            "id": 1,
            "slug": "cms",
            "name": "CMS"
          }
        ],
        "versions": [
          "3.0.0"
        ],
        "trafficRank": 1000,
        "confirmedAt": 1612824037,
      }
    ]
  },
  {
    "url": "https://example.org",
    "technologies": [], // No results available
    "crawl": true // Crawl initiated
  }
]
</Code></pre>
        </v-card-text>

        <v-divider />

        <v-card-title class="subtitle-2">
          Example response (error)
        </v-card-title>
        <v-card-text>
          <pre><Code>[
  {
    "url": "https://example.com",
    "errors": [
      "Something went wrong"
    ]
  }
]</Code></pre>
        </v-card-text>

        <v-divider />

        <v-card-title class="subtitle-2">
          Example callback response
        </v-card-title>
        <v-card-text>
          <p>
            The callback URL will receive a POST request when results become
            available. The callback URL will be invoked seperately for each
            requested URL.
          </p>

          <pre><Code>{
  "url": "https://example.com",
  "technologies": [
    {
      "slug": "craft-cms",
      "name": "Craft CMS",
      "versions": [
        "3.0.0"
      ],
      "categories": [
        {
          "id": 1,
          "slug": "cms",
          "name": "CMS"
        }
      ]
    }
  ]
}</Code></pre>
        </v-card-text>
      </v-card>

      <v-card class="mb-4">
        <v-card-title class="subtitle-2"> Example request </v-card-title>
        <v-card-text>
          <p>
            In this example we set <code>squash</code> to <code>false</code> to
            get results grouped by month. This is useful to see changes to the
            technology stack over time. We set <code>max_age</code> to
            <code>12</code> to get up to a year's worth of data (subject to
            availability).
          </p>

          <pre><Code>curl -H "x-api-key: &lt;your api key&gt;" "https://api.wappalyzer.com/lookup/v2/?urls=https://example.com&amp;callback_url=https://yourdomain.com&amp;squash=false&amp;max_age=12"</Code></pre>
        </v-card-text>

        <v-divider />

        <v-card-title class="subtitle-2"> Example response </v-card-title>
        <v-card-text>
          <pre><Code>[
  {
    "url": "https://example.com",
    "results": [
      {
        "monthYear": "01-2020", // The month in which the technologies were indentified
        "technologies": [
          {
            "slug": "craft-cms",
            "name": "Craft CMS",
            "categories": [
              {
                "id": 1,
                "slug": "cms",
                "name": "CMS"
            ],
            "versions": [
              "3.0.0"
            ],
            "trafficRank": 1000
            "confirmedAt": 1612824037,
          }
        ]
      },
      {
        "monthYear": "02-2020",
        "technologies": [
          ...
        ]
      }
    ]
  }
]</Code></pre>
        </v-card-text>
      </v-card>
    </Page>
  </div>
</template>

<script>
import { mdiLightbulbOnOutline } from '@mdi/js'

import Page from '~/components/Page.vue'
import Heading from '~/components/Heading.vue'
import Code from '~/components/Code.vue'
import side from '~/assets/json/nav/docs.json'

export default {
  components: {
    Page,
    Heading,
    Code,
  },
  data() {
    return {
      title: 'Lookup API',
      side,
      crumbs: [
        { title: 'Developer documentation', to: '/docs/' },
        { title: 'APIs', to: '/docs/api/' },
      ],
      mdiLightbulbOnOutline,
    }
  },
}
</script>

<style>
td {
  padding-top: 0.2rem !important;
  padding-bottom: 0.2rem !important;
}
</style>
