<template>
  <v-container fluid>
<!--    <v-row>-->
<!--      <v-col cols="12" lg="6">-->
<!--        <SectorialChart />-->
<!--      </v-col>-->
<!--      <v-col cols="12" lg="6">-->
<!--        <SectorialIndices />-->
<!--      </v-col>-->
<!--    </v-row>-->
    <v-row>
      <v-col cols="12">
        <ShortListedStocks
            :shortlist-offset="shortlistLOffset"
            :key="randomNumber"
            @no-more-shortlisted-stocks-event="disableButton"
        />
        <v-row justify="start">
          <v-col>
            <v-btn
              color="secondary"
              dark
              small
              class="ma-2"
              @click="loadMoreShortListedStocks()"
              :disabled="previousButtonDisabled"
            >
              Previous
            </v-btn>
            <v-btn
                color="secondary"
                dark
                small
                class="ma-2"
                @click="loadLessShortListedStocks()"
                :disabled="nextButtonDisabled"
            >
              Next
            </v-btn>
          </v-col>
          <v-spacer />
        </v-row>
      </v-col>
      <v-spacer/>
    </v-row>
  </v-container>
</template>

<script>
import ShortListedStocks from "@/components/ShortListedStocks";
// import SectorialChart from "@/components/SectorialChart";
// import SectorialIndices from "@/components/SectorialIndices";

export default {
  name: "DashboardPage",
  components: {
    ShortListedStocks,
    // SectorialChart,
    // SectorialIndices,
  },
  data() {
    return {
      shortlistLOffset: 0,
      randomNumber: 0,
      nextButtonDisabled: true,
      previousButtonDisabled: false,
    };
  },
  methods: {
    loadMoreShortListedStocks() {
      this.shortlistLOffset += 1;
      this.randomNumber = Math.random();
      this.nextButtonDisabled = false;
    },
    loadLessShortListedStocks() {
      this.shortlistLOffset -= 1;
      this.randomNumber = Math.random();
      this.previousButtonDisabled = false;
    },
    disableButton(offsetValue) {
      // if offsetValue is a negative number, then disable the previous button
      // else disable the next button
      if (offsetValue > 0) {
        this.previousButtonDisabled = true;
      } else if (offsetValue < 0){
        this.nextButtonDisabled = true;
      }
    }
  }
}
</script>

<style scoped>

</style>
