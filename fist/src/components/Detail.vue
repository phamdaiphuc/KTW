<template>
    <Page>
        <ActionBar >
            <StackLayout orientation="horizontal" backgroundColor="white" width="70%" borderRadius="50px">
               <TextField  width="200px" height="40%" fontSize="14" hint="Nhan Vao Day " />
               <Image src="~/assets/images/saw.jpg" width="50" height="50" marginLeft="140"   @tap="ShowCart()"/>
            </StackLayout>
        </ActionBar>
        <ListView for="obj in drinks" @itemTap="onItemTap">
            <v-template>
                    <FlexboxLayout flexDirection="row">
                    <StackLayout orientation="vertical">

                        <Label :text="obj.header" color="#FF0000" backgroundColor="lightgray" />
                        <GridLayout :key="item.name" v-for="item in obj.items" columns="auto,*,auto,auto" rows="auto,25" 
                         verticalAlignment="top">
                              <!-- cot mot -->
                            <Image :src="item.imgsrc" col="0" horizontalAlignment="left" verticalAlignment="bottom" margin="3" />
                                <!-- cot thu hai de name-->
                            <Label :text="item.name" col="1" horizontalAlignment="left" verticalAlignment="bottom" margin="3" />
                            <!-- cot ba -->
                            <Label :text="item.price" col="2" horizontalAlignment="left" verticalAlignment="bottom" margin="3" />
                            <!-- cot bon -->
                            <Button text="Mua" col="3" @tap="addCart(item)"/>
                        </GridLayout>
                    </StackLayout>
                    </FlexboxLayout>
            </v-template>
        </ListView>






    </Page>
</template>
<script>
import Cart from "./Cart.vue"
export default {
    data() 
    { 
        return{
            // thuoc tinh mot
            drinks: [
        {
          header: "Non Alcoholic Drinks",
          items: [
            {
              imgsrc: "~/assets/images/dCappuccino.jpg",
              name: "Cappuccino",
              quantity:1,
              price: "3",
            },
            {
              imgsrc: "~/assets/images/dCoffee.jpg",
              name: "Coffee",
              quantity:1,
              price: "2.6",
            },
            {
              imgsrc: "~/assets/images/dCola.jpg",
              name: "Coca Cola",
              quantity:1,
              price: "3.5",
            },
            {
              imgsrc: "~/assets/images/dMilk.jpg",
              name: "Milk",
              quantity:1,
              price: "2.5",
            },
            {
              imgsrc: "~/assets/images/dPepsi.jpg",
              name: "Pepsi",
              quantity:1,
              price: "3.5",
            },
            {
              imgsrc: "~/assets/images/dTea.jpg",
              name: "Tea",
              quantity:1,
              price: "3",
            },
            {
              imgsrc: "~/assets/images/dWater.jpg",
              name: "Water",
              quantity:1,
              price: "2",
            },
          ],
        },
        {
          header: "Alcoholic Drinks",
          items: [
            {
              imgsrc: "~/assets/images/dBeer.jpg",
              name: "Beer",
              quantity:1,
              price: "3",
            },
            {
              imgsrc: "~/assets/images/dGin.jpg",
              name: "Gin",
              quantity:1,
              price: "4",
            },
            {
              imgsrc: "~/assets/images/dMartini.jpg",
              name: "Martini",
              quantity:1,
              price: "4.5",
            },
            {
              imgsrc: "~/assets/images/dRum.jpg",
              name: "Rum",
              quantity:1,
              price: "5",
            },
            {
              imgsrc: "~/assets/images/dWine.jpg",
              name: "Wine",
              quantity:1,
              price: "4.5",
            },
            {
              imgsrc: "~/assets/images/dWhiskey.jpg",
              name: "Whiskey",
              quantity:1,
              price: "6",
            },
          ],
        
        },
      ] ,
            //thuoc tinh hai
              cart:[],
        }
        
      
    },
    //method 
    methods:{
        addCart(obj)
    {
      //nếu gio hàng trống
      var flag=false;
      if(this.cart.length<0)
      {
        flag=false;
      }
      // nếu giỏ hàng có hàng, thì xem trong giỏ hàng có trùng món hay không, nếu trùng thì cho true
      else{
        for(var i=0;i<this.cart.length;i++)
        {
          // nếu mà đối tượng mà mình chọn có name=name trong giỏ hàng thì cho lại true
          if(obj.name==this.cart[i].name)
          {
            flag=true;
          }
        }
      }
      // trường họp flag=false
      if(flag==false)
      {
        this.cart.push(obj);
      }
      // ngược lại tức là hàng đã có, duyệ lại trong giỏ hàng
      // nếu đối tượng mà mình chọn có name=name trong giỏ hang thì tằng số lượng lên
      else{
        for(var i=0;i<this.cart.length;i++)
        {
          // nếu mà đối tượng mà mình chọn có name=name trong giỏ hàng thì cho lại true
          if(obj.name==this.cart[i].name)
          {
            this.cart[i].quantity+=1;
          }
        }
      }
      
    },
        ShowCart(){
        this.$navigateTo(Cart,{
            props:{
                cart:this.cart,
            }
        })
    }
    },
   
    //computed
        
    
}
</script>
<style csoped>
   
</style>