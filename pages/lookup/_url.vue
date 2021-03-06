<template>
  <Page :title="title" :seo-title="seoTitle" :head="meta" no-heading>
    <div class="mt-6 mb-6">
      <v-btn to="/apps/" class="mb-2 mr-2" depressed>
        <v-icon left>
          {{ mdiPuzzle }}
        </v-icon>
        Browser extension
      </v-btn>
      <v-btn to="/apps/" class="mb-2 mr-2" depressed>
        <v-icon left>
          {{ mdiPowerPlug }}
        </v-icon>
        CRM integration
      </v-btn>
      <v-btn to="/api/" class="mb-2" depressed>
        <v-icon left>
          {{ mdiConsole }}
        </v-icon>
        API
      </v-btn>
    </div>

    <v-card class="mb-4">
      <v-tabs
        v-model="tab"
        slider-color="primary"
        background-color="secondary"
        active-class="primary--text"
      >
        <v-tab><small>Single website</small></v-tab>
        <v-tab><small>Multiple websites</small></v-tab>
      </v-tabs>

      <v-divider />

      <v-tabs-items v-model="tab">
        <v-tab-item eager>
          <v-card-title>
            <v-row align="center">
              <v-col cols="12" sm="4" class="pb-0">
                <div class="d-flex align-center">
                  <v-icon color="primary" left>
                    {{ mdiLayersOutline }}
                  </v-icon>
                  Lookup
                </div>
              </v-col>
              <v-col cols="12" sm="8" class="pb-0">
                <Credits />
              </v-col>
            </v-row>
          </v-card-title>

          <v-card-text>
            <Url ref="url" :url="url" class="mt-4" @change="submit" />

            <v-alert v-if="error" type="info" class="mt-4 mb-0" prominent text>
              {{ error }}
            </v-alert>

            <v-card v-if="loading" class="mt-4" flat>
              <v-card-text class="d-flex justify-center pa-12">
                <v-progress-circular
                  :size="100"
                  color="primary"
                  width="5"
                  style="opacity: 0.2"
                  indeterminate
                ></v-progress-circular>
              </v-card-text>
            </v-card>

            <v-expansion-panels
              v-if="
                !loading &&
                !error &&
                (Object.keys(attributes).length || keywords.length)
              "
              class="mt-4"
            >
              <Attributes
                v-if="Object.keys(attributes).length"
                :hostname="attributes"
                :masked-sets="maskedSets"
                @signIn="signInDialog = true"
              />

              <v-expansion-panel v-if="keywords && keywords.length" flat>
                <v-expansion-panel-header
                  class="subtitle-2"
                  style="line-height: 1em"
                >
                  Keywords
                </v-expansion-panel-header>
                <v-expansion-panel-content eager>
                  <v-chip-group column>
                    <v-chip
                      v-for="keyword in keywords"
                      :key="keyword"
                      :to="`/websites/${keyword}/`"
                      color="accent--text"
                      outlined
                      label
                    >
                      {{ keyword }}
                    </v-chip>
                  </v-chip-group>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>

            <v-card v-if="!loading && technologies.length" class="mt-4">
              <v-card-title class="subtitle-2" style="line-height: 1em">
                Technologies
              </v-card-title>
              <v-card-text class="px-0">
                <v-simple-table>
                  <tbody>
                    <tr v-for="category in categorised" :key="category.slug">
                      <td>
                        <div
                          v-for="{
                            name,
                            slug,
                            categories,
                            versions,
                            icon,
                          } in category.technologies"
                          :key="name"
                          class="d-flex align-center"
                        >
                          <nuxt-link
                            :to="`/technologies/${
                              categories.length ? `${categories[0].slug}/` : ''
                            }${slug}/`"
                            class="d-inline-flex align-center body-2 my-2"
                          >
                            <TechnologyIcon :icon="icon" />
                            {{ name }}
                          </nuxt-link>

                          <v-chip
                            v-for="version in versions.slice(-3)"
                            :key="version"
                            class="ml-2 text--disabled"
                            color="secondary"
                            small
                            label
                          >
                            {{ version }}
                          </v-chip>
                        </div>
                      </td>
                      <th class="text-right font-weight-regular">
                        <nuxt-link
                          :to="`/technologies/${category.slug}/`"
                          class="text--disabled"
                        >
                          {{ category.name }}
                        </nuxt-link>
                      </th>
                    </tr>
                  </tbody>
                </v-simple-table>
              </v-card-text>
            </v-card>
          </v-card-text>
        </v-tab-item>

        <v-tab-item eager>
          <v-card-title>
            <v-row align="center">
              <v-col class="pb-0 flex-grow-1 flex-shrink-0">
                <div class="d-flex align-center">
                  <v-icon color="primary" left>
                    {{ mdiLayersOutline }}
                  </v-icon>
                  Bulk lookup
                </div>
              </v-col>
              <v-col class="pb-0 flex-grow-0 flex-shrink-1">
                <v-btn
                  color="primary primary--text lighten-1"
                  depressed
                  small
                  @click="$refs.pricingDialog.open()"
                >
                  <v-icon left>
                    {{ mdiCalculator }}
                  </v-icon>
                  Pricing
                </v-btn>
              </v-col>
            </v-row>
          </v-card-title>
          <v-card-text class="pt-4">
            <p style="max-width: 600px">
              Supply your own list of websites and we'll report back with the
              technologies they use, as well as any metadata we find. On a
              <v-chip to="/pro/" color="primary" x-small outlined> PRO </v-chip>
              plan, company and contact information is included where available.
            </p>

            <p class="mb-6" style="max-width: 600px">
              The resulting list is in CSV and JSON format (<a
                href="/bulk-sample.zip"
                download
                >sample</a
              >).
            </p>

            <v-card class="mb-4">
              <v-card-title class="subtitle-2">
                Upload a list of websites
              </v-card-title>
              <v-card-text>
                <p class="mb-6">
                  Upload a .txt file with up to 100,000 URLs, each on a separate
                  line.<br />
                </p>

                <v-file-input
                  :error-messages="fileErrors"
                  :hint="
                    file
                      ? `${file.split('\n').length.toLocaleString()} URLs`
                      : ''
                  "
                  persistent-hint
                  placeholder="Select a file..."
                  accept="text/plain"
                  hide-details="auto"
                  background-color="white"
                  outlined
                  @change="fileChange"
                />

                <v-checkbox
                  v-model="removeInvalid"
                  v-if="removeInvalid || fileErrors.length"
                  label="Remove invalid URLs"
                  hide-details="auto"
                />
              </v-card-text>
            </v-card>

            <v-expansion-panels class="mb-4">
              <v-expansion-panel ref="compliance">
                <v-expansion-panel-header class="subtitle-2">
                  Compliance
                  <span class="body-2">
                    <v-chip color="primary" class="ml-2" x-small outlined
                      >PRO</v-chip
                    >
                  </span>
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                  <Pro class="mx-n6 mb-4" small />

                  <v-radio-group
                    v-model="compliance"
                    class="my-0"
                    :disabled="!isPro"
                    mandatory
                  >
                    <v-radio
                      value="include"
                      class="mt-0"
                      hide-details
                      :disabled="australia"
                    >
                      <template #label> Include contact details </template>
                    </v-radio>
                    <v-radio
                      value="excludeEU"
                      class="mt-0"
                      hide-details
                      :disabled="!isPro || australia"
                    >
                      <template #label>
                        Exclude contact details of EU websites
                      </template>
                    </v-radio>
                    <v-radio value="exclude" class="mt-0" hide-details>
                      <template #label> Exclude all contact details </template>
                    </v-radio>
                  </v-radio-group>

                  <v-checkbox
                    v-model="australia"
                    label="I'm in or do business in Australia"
                    class="mt-0"
                    :disabled="!isPro"
                    hide-details
                  />

                  <v-alert
                    color="secondary"
                    border="left"
                    class="mt-8 mb-2"
                    dense
                  >
                    <small>
                      We're unable to supply email addresses and phone numbers
                      if you're in Australia or carry on business or activities
                      in Australia.
                    </small>
                  </v-alert>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>

            <v-card
              v-if="!isPro"
              color="primary lighten-1 primary--text"
              class="mb-4"
              flat
            >
              <v-card-title class="subtitle-2">
                <v-icon color="primary" size="20" left>
                  {{ mdiLockOpenVariantOutline }}
                </v-icon>
                Unlock pro features
              </v-card-title>
              <v-card-text class="primary--text pb-0">
                Subscribe to a
                <v-chip to="/pro/" color="primary" x-small outlined>
                  PRO
                </v-chip>
                plan to include company and contact information in lookups.
              </v-card-text>
              <v-card-actions>
                <v-spacer />

                <v-btn to="/pricing/" color="primary" text>
                  Compare plans
                  <v-icon right>
                    {{ mdiArrowRight }}
                  </v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>

            <v-btn
              :disabled="!!(!file || fileErrors.length)"
              :loading="ordering"
              color="primary"
              large
              depressed
              @click="submitBulk"
            >
              Get a quote
              <v-icon right>
                {{ mdiArrowRight }}
              </v-icon>
            </v-btn>
          </v-card-text>
        </v-tab-item>
      </v-tabs-items>
    </v-card>

    <v-dialog
      v-if="!isLoading && !isSignedIn"
      v-model="signInDialog"
      max-width="400px"
    >
      <SignIn mode-sign-up mode-continue />
    </v-dialog>

    <PricingDialog ref="pricingDialog" product="bulk" />
  </Page>
</template>

<script>
import { mapState, mapActions } from 'vuex'
import {
  mdiLayersOutline,
  mdiMagnify,
  mdiCalculator,
  mdiArrowRight,
  mdiLockOpenVariantOutline,
  mdiPuzzle,
  mdiConsole,
  mdiPowerPlug,
} from '@mdi/js'

import Page from '~/components/Page.vue'
import TechnologyIcon from '~/components/TechnologyIcon.vue'
import Credits from '~/components/Credits.vue'
import Url from '~/components/Url.vue'
import Attributes from '~/components/Attributes.vue'
import SignIn from '~/components/SignIn.vue'
import PricingDialog from '~/components/PricingDialog.vue'
import Pro from '~/components/Pro.vue'
import { lookup as meta } from '~/assets/json/meta.json'
import sets from '~/assets/json/sets.json'

function getFullUrl(url) {
  if (!url) {
    return null
  }

  let fullUrl

  try {
    new URL(url) // eslint-disable-line no-new

    return url
  } catch (error) {
    if (url.includes('.')) {
      if (url.startsWith('www.')) {
        fullUrl = `http://${url}`
      } else {
        fullUrl = `http://${url.split('.').length > 2 ? '' : 'www.'}${url}`
      }

      new URL(fullUrl) // eslint-disable-line no-new

      return fullUrl
    }
  } finally {
    // Continue
  }

  return null
}

export default {
  components: {
    Page,
    TechnologyIcon,
    Credits,
    Url,
    Attributes,
    SignIn,
    PricingDialog,
    Pro,
  },
  async asyncData({
    route,
    $axios,
    store: {
      state: {
        user: { isSignedIn },
      },
    },
  }) {
    const { url } = route.params

    const fullUrl = getFullUrl(url)

    if (fullUrl) {
      try {
        const { maskedSets, technologies, attributes, keywords } = (
          await $axios.get(
            `lookup-site${isSignedIn ? '' : '/public'}/${encodeURIComponent(
              fullUrl
            )}`
          )
        ).data

        return {
          url: fullUrl,
          lastUrl: fullUrl,
          maskedSets,
          technologies,
          attributes,
          keywords,
        }
      } catch (error) {
        if (error.response && error.response.status === 401) {
          return { url: fullUrl, lastUrl: fullUrl, signInDialog: true }
        }

        return {
          url: fullUrl,
          lastUrl: fullUrl,
          error: error.message || error.toString(),
        }
      }
    } else if (url) {
      return { url, lastUrl: url }
    }
  },
  data() {
    return {
      title: 'Technology lookup',
      australia: false,
      compliance: 'include',
      error: false,
      file: '',
      fileErrors: [],
      inputFile: null,
      loading: false,
      removeInvalid: false,
      meta,
      sets,
      attributes: {},
      keywords: [],
      maskedSets: [],
      mdiLayersOutline,
      mdiMagnify,
      mdiCalculator,
      mdiArrowRight,
      mdiLockOpenVariantOutline,
      mdiPuzzle,
      mdiConsole,
      mdiPowerPlug,
      order: false,
      ordering: false,
      url: '',
      lastUrl: '',
      signInDialog: false,
      tab: null,
      technologies: [],
    }
  },
  computed: {
    ...mapState({
      user: ({ user }) => user.attrs,
      isLoading: ({ user, credits }) =>
        user.loading || (user.signingIn && credits.loading),
      isPro: ({ credits }) => credits.pro,
      isSignedIn: ({ user }) => user.isSignedIn,
      credits: ({ credits: { credits } }) => credits,
    }),
    seoTitle() {
      const fullUrl = getFullUrl(this.url)

      if (fullUrl) {
        const { hostname } = new URL(fullUrl)

        return `Technologies used on ${hostname.replace(/^www\./, '')}`
      }

      return 'Technology lookup'
    },
    categorised() {
      return Object.values(
        this.technologies.reduce((categories, technology) => {
          technology.categories.forEach((category) => {
            categories[category.slug] = categories[category.slug] || {
              ...category,
              technologies: [],
            }

            categories[category.slug].technologies.push(technology)
          })

          return categories
        }, {})
      )
    },
  },
  watch: {
    async isSignedIn() {
      if (this.isSignedIn) {
        if (this.user?.billingCountry?.toLowerCase() === 'au') {
          this.australia = true
        }

        this.signInDialog = false

        this.technologies = []
        this.attributes = {}
        this.keywords = []

        await this.getCredits()

        if (this.tab === 0 && this.url) {
          this.lastUrl = null

          this.submit()
        }

        if (this.tab === 1 && this.ordering) {
          this.submitBulk()
        }

        this.compliance = this.isPro && !this.australia ? 'include' : 'exclude'
      }
    },
    isLoading() {
      if (!this.isLoading) {
        this.compliance = this.isPro && !this.australia ? 'include' : 'exclude'
      }
    },
    url() {
      const fullUrl = getFullUrl(this.url)

      if (fullUrl) {
        const { hostname } = new URL(fullUrl)

        history.pushState({}, null, `/lookup/${hostname.replace(/^www\./, '')}`)
      }
    },
    tab(index) {
      if (index === 1) {
        if (this.$route.hash !== '#bulk') {
          this.$router.replace({ path: '/lookup/', hash: '#bulk' })
        }
      } else if (this.$route.hash === '#bulk') {
        this.$router.replace({ path: '/lookup/' })
      }
    },
    australia() {
      if (this.australia) {
        this.compliance = 'exclude'
      }
    },
    removeInvalid() {
      this.fileChange()
    },
  },
  async mounted() {
    if (this.$route.hash === '#bulk') {
      this.tab = 1
    }

    if (this.isSignedIn) {
      if (this.user?.billingCountry?.toLowerCase() === 'au') {
        this.australia = true
      }

      try {
        await this.getCredits()
      } catch (error) {
        this.error = this.getErrorMessage(error)
      }
    }

    if (!this.isLoading) {
      if (!this.isLoading) {
        this.compliance = this.isPro && !this.australia ? 'include' : 'exclude'
      }
    }

    if (this.url && this.$refs.url && !this.technologies.length) {
      this.$refs.url.search()
    }
  },
  methods: {
    ...mapActions({
      getCredits: 'credits/get',
    }),
    async submit(url = this.url) {
      url = getFullUrl(url) || url

      if (!url || (url === this.lastUrl && this.technologies.length)) {
        return
      }

      this.url = url

      try {
        const { hostname } = new URL(url) // eslint-disable-line no-new

        if (
          /^(?:[\d.]+|(?:[a-f0-9:]+:+)+[a-f0-9]+|localhost)$/.test(hostname)
        ) {
          throw new Error('Invalid URL')
        }

        if (
          [
            'wappalyzer',
            'google',
            'facebook',
            'twitter',
            'reddit',
            'yahoo',
            'wikipedia',
            'amazon',
            'youtube',
          ].some((ignore) => hostname.includes(ignore))
        ) {
          this.error =
            'This website is excluded from lookups for technical reasons. Please use our free browser extension instead.'

          return
        }
      } catch (error) {
        this.error = 'Please enter a valid URL, including http:// or https://'

        return
      }

      this.lastUrl = url

      this.error = false

      if (this.isSignedIn) {
        if (!this.credits) {
          this.error = 'Insufficient credits.'

          return
        }
      }

      this.technologies = []
      this.attributes = {}
      this.keywords = []

      this.loading = true

      let credits

      try {
        if (this.isSignedIn) {
          ;({
            maskedSets: this.maskedSets,
            credits,
            technologies: this.technologies,
            attributes: this.attributes,
            keywords: this.keywords,
          } = (
            await this.$axios(`lookup-site/${encodeURIComponent(url)}`)
          ).data)
        } else {
          try {
            ;({
              maskedSets: this.maskedSets,
              technologies: this.technologies,
              attributes: this.attributes,
              keywords: this.keywords,
            } = (
              await this.$axios(`lookup-site/public/${encodeURIComponent(url)}`)
            ).data)
          } catch (error) {
            if (error.response && error.response.status === 401) {
              this.signInDialog = true
              this.loading = false

              return
            }

            throw error
          }
        }

        this.$store.commit('credits/setCredits', credits)
      } catch (error) {
        this.error =
          (error.response &&
            error.response.data &&
            (error.response.data.message || error.response.data)) ||
          this.getErrorMessage(error)
      }

      this.technologies = this.technologies || []
      this.attributes = this.attributes || {}
      this.keywords = this.keywords || []

      this.loading = false
    },
    async submitBulk() {
      this.ordering = true

      if (!this.$store.state.user.isSignedIn) {
        this.signInDialog = true

        return
      }

      try {
        const { id } = (
          await this.$axios.put('orders', {
            product: 'Technology lookup',
            bulk: {
              input: this.file,
              sets: this.sets
                .filter(({ disabled, value }) => value && !disabled)
                .map(({ key }) => key),
              compliance: this.compliance,
            },
          })
        ).data

        this.$router.push(`/orders/${id}`)
      } catch (error) {
        this.error = this.getErrorMessage(error)
      }

      this.ordering = false
    },

    async fileChange(file = this.inputFile) {
      this.inputFile = file

      this.file = ''
      this.fileErrors = []

      if (!file) {
        return
      }

      this.file = (await file.text())
        .trim()
        .split(/[\r\n]/)
        .filter((line) => line)
        .map((line, i) => {
          const url = !/^https?:\/\//.test(line.trim())
            ? `http://${line.trim()}`
            : line.trim()

          try {
            new URL(url) // eslint-disable-line no-new
          } catch (error) {
            if (this.removeInvalid) {
              return null
            } else {
              this.fileErrors.push(`Invalid URL on line ${i + 1}: ${line}`)
            }
          }

          return url
        })
        .filter((line) => line)

      this.fileErrors = this.fileErrors.slice(0, 10)

      if (this.file.length > 100000) {
        this.fileErrors.push('Limit of 100,000 URLs exceeded')
      }

      this.file = this.file.join('\n')
    },
  },
}
</script>
