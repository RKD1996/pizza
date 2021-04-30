<template>
  <div class="pizza-app">
    <div class="order-table">
      <div class="orders">
        <v-card class="items" max-width="344" v-for="od in orders"  :key="od.id">
          <v-card-title>
            Id: {{od.id}} - {{new Date() | filterDate}}
            <span :class="'status ' + od.status">{{od.status | filterStatus}}</span>
          </v-card-title>

          <v-card-text>
            <p class="param"> <b>Name</b> : {{od.name}}</p>
            <p class="param"> <b>Address</b> : {{od.address}}</p>
            <p class="param"> <b>No. of Items</b> : {{od.package.length}}</p>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="dialog = true; viewOrder = od;">view order</v-btn>
          </v-card-actions>
        </v-card>
        <v-dialog v-model="dialog" max-width="500">
          <v-card>
            <v-card-title class="headline">
              Order Details
              <v-spacer></v-spacer>
              <v-btn color="red darken-1" text @click="dialog = false">
                close
              </v-btn>
            </v-card-title>
            <v-card-text class="order-sum">
              <p> <span><b>Order Id</b></span> <span>{{viewOrder.id}}</span> </p>
              <p> <span><b>Name</b></span> <span>{{viewOrder.name}}</span> </p>
              <p> <span><b>Address</b></span> <span>{{viewOrder.address}}</span> </p>
              <p> <span> <b>Status</b> </span>
                <span>
                  <v-select
                    :items="status"
                    label="Change Status"
                    v-model="viewOrder.status"
                  ></v-select>
                </span>
              </p>
              <label for="order-details"> <b>Order Items</b> </label>
              <ul id="order-details">
                <li> <span> Food Name </span> <span> Size </span> <span> Qty </span> <span> Price </span> </li>
                <li v-for="vo in viewOrder.package"  :key="vo.id"> <span>{{vo.name}}</span> <span>{{vo.size}}</span> <span>{{vo.qty}}</span> <span>{{vo.price * vo.qty}}</span> </li>
                <li class="sum" > <span>CGST(2.5%)</span> <span>{{(viewOrder.total * 0.025)}}</span> </li>
                <li class="sum"> <span>SGST(2.5%)</span> <span>{{(viewOrder.total * 0.025)}}</span> </li>
                <li class="sum"> <span>Total</span> <span>{{(viewOrder.total * 0.025) + (viewOrder.total * 0.025) + viewOrder.total}}</span> </li>
              </ul>
            </v-card-text>
            <v-card-actions>

            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </div>
  </div>
</template>

<script>

  export default {
    name: 'Home',
    data () {
      return {
        dialog: '',
        viewOrder: {},
        status: [{text: 'Order Received', value: 'order_received'}, {text: 'Preparing', value: 'preparing'}, {text: 'Ready to Serve', value: 'ready_to_serve'}],
        orders: [
          {
            id: 1,
            name: 'Tausiq Parkar',
            status: 'order_received',
            address: '11 /, S G Road, Kalbadevi,  Mumbai,  Maharashtra, 400002',
            total: 457,
            package: [
              {
                id: 101,
                name: 'Margherita',
                size: 'medium',
                qty: 1,
                price: 199
              },
              {
                id: 111,
                name: 'Creamy Tomato Pasta Veg',
                size: 'small',
                qty: 2,
                price: 129
              }
            ]
          },
          {
            id: 2,
            name: 'Ishani Shah',
            status: 'order_received',
            address: '6 b, , Shreeji Bhuvan, Mangaldas Road, Chira Bazar,  Mumbai,  Maharashtra, 400002',
            total: 1330,
            package: [
              {
                id: 114,
                name: 'Peppy Paneer',
                size: 'large',
                qty: 2,
                price: 561
              },
              {
                id: 178,
                name: 'Garlic Bread',
                size: 'regular',
                qty: 1,
                price: 109
              },
              {
                id: 178,
                name: 'Coca Cola',
                size: '750 ml',
                qty: 1,
                price: 99
              }
            ]
          },
          {
            id: 3,
            name: 'Hetal Mitter',
            status: 'order_received',
            address: '142 , Bambukhana Bldg, Kalbadevi Rd, Kalbadevi,  Mumbai,  Maharashtra, 400002',
            total: 1284,
            package: [
              {
                id: 114,
                name: 'Pepper Barbecue Chicken',
                size: 'large',
                qty: 1,
                price: 699
              },
              {
                id: 178,
                name: 'Garlic Bread',
                size: 'regular',
                qty: 3,
                price: 109
              },
              {
                id: 178,
                name: 'Coca Cola',
                size: '1l',
                qty: 2,
                price: 129
              }
            ]
          },
          {
            id: 4,
            name: 'Skanda Aggarwal',
            status: 'order_received',
            address: '449 , F, Vasantwadi, Chira Bazar,  Mumbai,  Maharashtra, 400002',
            total: 5929,
            package: [
              {
                id: 114,
                name: 'Pepper Barbecue Chicken',
                size: 'large',
                qty: 6,
                price: 699
              },
              {
                id: 178,
                name: 'Garlic Bread',
                size: 'regular',
                qty: 10,
                price: 109
              },
              {
                id: 178,
                name: 'Coca Cola',
                size: '1l',
                qty: 5,
                price: 129
              }
            ]
          },
          {
            id: 5,
            name: 'Ravana Bahl',
            status: 'order_received',
            address: '412 /f, Dabholkar Wadi, Kalbadevi,  Mumbai,  Maharashtra, 400002',
            total: 702,
            package: [
              {
                id: 114,
                name: 'Creamy Tomato Pasta Veg',
                size: 'large',
                qty: 3,
                price: 234
              }
            ]
          }
        ],
      }
    },
    filters: {
      filterStatus (val) {
        let res = val.split('_')
        if (res.length == 2) {
          return res[0]+' '+res[1]
        }
        if (res.length == 3) {
          return res[0]+' '+res[1]+' '+res[2]
        }
        if (res.length == 1) {
          return res[0]
        }
      },
      filterDate(val) {
        let ts = `${val.getHours()}:${val.getMinutes()}`
        let H = +ts.substr(0, 2);
        let h = (H % 12) || 12;
        h = (h < 10)?("0"+h):h;  // leading 0 at the left for 1 digit hours
        let ampm = H < 12 ? " AM" : " PM";
        ts = h + ':' + ts.substr(2, 3) + ampm;
        return ts;
      }
    },
    methods: {
      viewOrder(val) {
        console.log(val);
      }
    }
  }
</script>
<style lang="scss">
  .pizza-app {
    .order-table {
      .orders {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        .items {
          margin: 7px;
          position: relative;
          .status {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 12px;
            text-transform: capitalize;
            padding: 0px 10px;
            border-radius: 25px;
            &.order_received{
              background: #FFCDD2;
            }
            &.preparing{
              background: #FFE0B2;
            }
            &.ready_to_serve{
              background: #DCEDC8;
            }
          }
          .param {
            margin: 0px;
          }
        }
      }
    }
  }

  .order-sum {
    p {
      margin: 0px;
      display: flex;
      align-items: center;
      border-bottom: 1px solid #ddd;
      span {
        flex-basis: 50%;
        padding: 3px 10px;
      }
    }
    #order-details {
      padding: 0px;
      list-style: none;
      li {
        display: flex;
        align-items: center;
        justify-content: center;
        font-style: 14px;
        span {
          flex-basis: 25%;
          height: 50px;
          display: flex;
          align-items: center;
          justify-content: center;
        }
        &:nth-child(1) {
          span {
            font-weight: bold;
          }
        }
        &.sum {
          span{
            height: 25px;
            &:nth-child(1) {
              flex-basis: 75%;
              font-weight: bold;
            }
          }
        }
      }
    }
  }
</style>
