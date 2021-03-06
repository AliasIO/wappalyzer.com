<template>
  <Page
    :title="title"
    :hero="{
      title: 'Wappalyzer has been upgraded',
      subtitle: release ? release.version : error ? '' : '...',
    }"
    :crumbs="false"
    no-head
  >
    <UseCases class="mb-10" />

    <v-row justify="center" class="my-4">
      <v-col cols="12" sm="8" lg="6" class="py-0">
        <v-card>
          <v-card-title>Changelog</v-card-title>

          <v-card-text v-if="error" class="px-0">
            <v-alert color="error" class="mx-4 mb-0" text>
              The changelog could not be loaded at this time.
            </v-alert>
          </v-card-text>
          <div
            v-if="!release && !error"
            class="d-flex justify-center py-2 pb-6"
          >
            <Progress />
          </div>
          <template v-if="release">
            <div v-for="type in ['add', 'fix', 'new']" :key="type">
              <template v-if="release.items[type].length">
                <v-card-title v-if="type === 'add'" class="subtitle-2">
                  <v-icon left>
                    {{ mdiPlusBox }}
                  </v-icon>
                  Additions
                </v-card-title>
                <v-card-title v-if="type === 'fix'" class="subtitle-2">
                  <v-icon left>
                    {{ mdiAutoFix }}
                  </v-icon>
                  Improvements
                </v-card-title>
                <v-card-title v-if="type === 'new'" class="subtitle-2">
                  <v-icon left>
                    {{ mdiStar }}
                  </v-icon>
                  Features
                </v-card-title>
                <v-card-text class="px-0">
                  <v-simple-table>
                    <tbody>
                      <tr
                        v-for="(item, index) in release.items[type]"
                        :key="index"
                      >
                        <td>{{ item }}</td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </v-card-text>
              </template>
            </div>
          </template>
        </v-card>
      </v-col>
    </v-row>
  </Page>
</template>

<script>
import {
  mdiPlusBox,
  mdiAutoFix,
  mdiStar,
  mdiFilterVariant,
  mdiPlay,
} from '@mdi/js'

import Page from '~/components/Page.vue'
import Progress from '~/components/Progress.vue'
import UseCases from '~/components/UseCases.vue'

export default {
  components: {
    Page,
    Progress,
    UseCases,
  },
  data() {
    return {
      title: 'Upgraded',
      mdiPlusBox,
      mdiAutoFix,
      mdiStar,
      release: null,
      error: false,
      mdiFilterVariant,
      mdiPlay,
      videoDialog: false,
    }
  },
  async mounted() {
    try {
      this.release = (await this.$axios.get(this.$config.RELEASE_URL)).data
    } catch (error) {
      this.error = this.getErrorMessage(error)
    }
  },
}
</script>
