<template>
  <v-container fluid>
    <v-card>
      <v-card-title>{{ $t("components.NetworkCard.Network") }}</v-card-title>
      <v-tabs
          v-model="settings.MinionDetail.NetworkCard.tab"
          @change="updateSettings"
      >
      <v-tabs-slider></v-tabs-slider>

        <v-tab href="#interface">
          {{ $t("components.NetworkCard.Interface") }}
        </v-tab>

        <v-tab href="#mac">
          {{ $t("components.NetworkCard.MAC") }}
        </v-tab>

        <v-tab href="#dns">
          {{ $t("components.NetworkCard.DNS") }}
        </v-tab>
      </v-tabs>
      <v-tabs-items v-model="settings.MinionDetail.NetworkCard.tab">
        <v-tab-item id="interface">
          <v-simple-table>
            <tbody>
              <tr v-for="(val, key) in minion.ip_interfaces" :key="key">
                <td>{{ key }}</td>
                <td class="text-right" v-for="(iface, k) in val" :key="k">{{ iface }}</td>
              </tr>
              <tr>
                <td>{{ $t("components.NetworkCard.IPV4Gateway") }}</td>
                <td class="text-right">{{ minion.ip4_gw }}</td>
              </tr>
              <tr>
                <td>{{ $t("components.NetworkCard.IPV6Gateway") }}</td>
                <td class="text-right">{{ minion.ip6_gw }}</td>
              </tr>
            </tbody>
          </v-simple-table>
        </v-tab-item>
        <v-tab-item id="mac">
          <v-simple-table>
            <tbody>
              <tr v-for="(val, key) in minion.hwaddr_interfaces" :key="key">
                <td>{{ key }}</td>
                <td class="text-right">{{ val }}</td>
              </tr>
            </tbody>
          </v-simple-table>
        </v-tab-item>
        <v-tab-item id="dns">
          <v-simple-table>
            <tbody>
              <tr v-for="(val, key) in minion.dns" :key="key">
                <td>{{ key }}</td>
                <td class="text-right">{{ val.length >= 1 ? val : "" }}</td>
              </tr>
            </tbody>
          </v-simple-table>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </v-container>
</template>

<script>
import { mapState } from "vuex"

export default {
  name: "NetworkCard",
  data() {
    return {
      tab: null,
      tabs: 3,
    };
  },
  props: ["minion"],
  methods: {
    updateSettings() {
      this.$store.commit("updateSettings")
    },
  },
  computed: {
    ...mapState({
      settings: state => state.settings,
    }),
  },
};
</script>

<style scoped></style>
