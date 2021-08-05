<template>
  <v-main class="appbackground application">
    <v-container fluid>
      <v-row>
        <v-col align="center" justify="center" cols="12">
          <blockquote style="color: white; font-size: xx-large">
            &#8220;Welcome {{validUserName}}!&#8221;
            <footer>
              <small>
                <em>Eagle Financial Services, your Midwest Financial Services Partner.</em>
              </small>
            </footer>
          </blockquote>
        </v-col>
      </v-row>
    </v-container>

    <v-container fluid>
      <v-row
        align="center"
        justify="center"
      >
        <v-col
          cols="12"
          sm="10"
          md="10"
        >
          <v-card class="elevation-2">
            <v-container
              fluid
              grid-list-md
            >
              <v-row>
                <v-col>
                  <v-card>
                    <v-img
                      :src="require('@/assets/images/customers.jpg')" height="200px">
                    </v-img>
                    <v-card-text>
                      <div class="blue--text text-h6">
                        Customers
                      </div>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn flat color="blue" @click="viewCustomers">View Details</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-col>
                <v-col>
                  <v-card>
                    <v-img
                      :src="require('@/assets/images/nonstock1.jpg')" height="200px">
                    </v-img>
                    <v-card-text class="custom-selector headline">
                      <div class="green--text text-h6" >
                        Investments
                      </div>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn flat color="green" @click="viewInvestments">View Details</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-col>
                <v-col>
                  <v-card>
                    <v-img
                      :src="require('@/assets/images/stocks1.jpg')" height="200px">
                    </v-img>
                    <v-card-text>
                      <div class="red--text text-h6">
                        Stocks
                      </div>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn flat color="red" @click="viewStocks">View Details</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-col>
              </v-row>
            </v-container>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<style scoped>
.appbackground {
  background: url('../assets/images/New.jpg');
  background-size: cover;


}
.application {
  font-family: "Font Family Name";
}
 em {
  font-style: italic;
  font-size: xx-large !important;
   color :white ;

}
</style>

<script>
import router from '../router';

export default {
  name: 'Home',
  data: () => ({
    validUserName: "Guest"
  }),
  mounted() {
    this.getUser();
  },
  methods: {
    viewCustomers() {
      router.push('/customer-list');
    },
    viewInvestments() {
      router.push('/investment-list');
    },
    viewStocks() {
      router.push('/stock-list');
    },
    getUser() {
      if (localStorage.getItem("isAuthenticates")
        && JSON.parse(localStorage.getItem("isAuthenticates")) === true) {
        this.validUserName = JSON.parse(localStorage.getItem("log_user"));
      }
    }
  }
}
</script>
