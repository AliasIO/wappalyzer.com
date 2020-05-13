<template>
  <v-container class="matrix__container mt-12 pl-0 pr-3 pt-2 pb-4">
    <v-row class="matrix" no-gutters>
      <v-col>
        <v-responsive
          :height="
            (Object.values(items).some(({ description }) => description)
              ? 100
              : 0) + (Object.keys(items).length > 1 ? 155 : 125)
          "
        />
        <template v-for="attr in attrs">
          <v-divider />
          <v-responsive :key="attr.text" height="60">
            <v-card-text>
              {{ attr.text }}
            </v-card-text>
          </v-responsive>
        </template>
      </v-col>
      <v-col
        v-for="(item, id) in items"
        :class="item.raised ? 'matrix__col--raised' : ''"
        :key="item.size"
      >
        <v-responsive v-if="!item.raised" height="20"> </v-responsive>
        <v-card :raised="item.raised" class="text-center">
          <v-responsive v-if="!item.raised" height="10"> </v-responsive>
          <v-responsive
            v-if="item.raised && Object.keys(items).length > 1"
            height="30"
          >
            <v-card-subtitle class="overline">
              {{ raisedText }}
            </v-card-subtitle>
          </v-responsive>
          <v-responsive height="60">
            <v-card-title class="justify-center">
              {{ item.name }}
            </v-card-title>
          </v-responsive>
          <v-responsive v-if="item.description" height="100">
            <v-card-subtitle>
              {{ item.description }}
            </v-card-subtitle>
          </v-responsive>
          <v-responsive height="65">
            <v-card-actions>
              <v-btn
                v-if="item.to"
                :to="item.to"
                :text="!item.raised"
                color="primary white-text"
                class="mx-auto"
                >{{ buttonText }}</v-btn
              >
              <v-btn
                v-else
                @click="$emit('select', id)"
                :text="!item.raised"
                color="primary white-text"
                class="mx-auto"
                >{{ buttonText }}</v-btn
              >
            </v-card-actions>
          </v-responsive>
          <template v-for="(attr, name) in attrs">
            <v-divider />
            <v-responsive height="60">
              <v-card-text :key="name" class="text-center">
                <template v-if="attr.type === 'currency'">
                  <template v-if="item.attrs[name]">
                    <span class="font-weight-medium">
                      {{ formatCurrency(item.attrs[name] / 100) }}
                    </span>
                    <template v-if="name === 'amount'">
                      / {{ item.interval }}
                    </template>
                  </template>
                  <template v-else>
                    Free
                  </template>
                </template>
                <template v-else-if="attr.type === 'number'">
                  <template v-if="item.attrs[name]">
                    {{ formatNumber(item.attrs[name]) }}
                  </template>
                  <template v-else>
                    Unlimited
                  </template>
                </template>
                <template v-else-if="attr.type === 'boolean'">
                  <v-icon v-if="item.attrs[name] === true" color="success">
                    mdi-check
                  </v-icon>
                  <small v-else>
                    {{ item.attrs[name] }}
                  </small>
                </template>
                <small v-else-if="attr.type === 'small'">
                  {{ item.attrs[name] }}
                </small>
                <template v-else>
                  {{ item.attrs[name] }}
                </template>
              </v-card-text>
            </v-responsive>
          </template>
          <v-responsive v-if="item.raised" height="20"> </v-responsive>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    items: {
      type: Object,
      default: () => {}
    },
    attrs: {
      type: Object,
      default: () => {}
    },
    buttonText: {
      type: String,
      default: 'Order'
    },
    raisedText: {
      type: String,
      default: 'Most popular'
    }
  }
}
</script>

<style>
.matrix {
  min-width: 850px;
}

.matrix__container {
  overflow-x: auto;
}

.matrix__col--raised {
  z-index: 2;
}
</style>