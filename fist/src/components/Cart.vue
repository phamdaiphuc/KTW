<template>
  <Page>
    <ActionBar marginBottom="20">
      <Image
        src="~/assets/images/saw.jpg"
        width="40"
        height="40"
        marginLeft="10"
      />
    </ActionBar>
    <StackLayout orientation="vertical">
      <GridLayout columns="50,*,90,80" verticalAlignment="top">
        <Label text="Ảnh" col="0" fontWeight="bold" />
        <Label text="Sản phẩm" col="1" fontWeight="bold" />
        <Label text="Số lượng" col="2" fontWeight="bold" />
        <Label text="Đơn giá" col="3" fontWeight="bold" />
      </GridLayout>
      <!-- GridLayout như là 1 table có dòng và cột -->
      <GridLayout :key="item.name" v-for="item in cart"
        columns="50,*,90,80" rows="auto, 25" verticalAlignment="top">
        <!-- cột đầu tiên để hình col = 0 -->
        <Image :src="item.imgsrc" col="0" verticalAlignment="bottom"/>

        <!-- cột thứ 2 để name col = 1 -->
        <Label :text="item.name" col="1" horizontalAlignment="left" verticalAlignment="bottom"/>

        <!-- cột thứ 3 để quantity col = 2 -->
        <Label :text="item.quantity" col="2" verticalAlignment="bottom"/>

        <!-- cột thứ 4 để price col = 3 -->
        <Label :text="item.price" col="3" verticalAlignment="bottom"/>
      </GridLayout>
      <GridLayout columns="50,*,90,80" rows="auto, 25" verticalAlignment="top">
        <Label text="Tổng" col="0" colSpan="2" fontWeight="bold" />
        <Label :text="itemCount" col="2" fontWeight="bold" />
        <Label :text="total" col="3" fontWeight="bold" />
      </GridLayout>
    </StackLayout>
  </Page>
</template>

<script>
export default {
  // nhận giỏ hàng được đưa tới
  props: ['cart'],
  data() {
    return {};
  },
  computed: {
    // tính tổng số lượng
    itemCount() {
      var tongsl = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tongsl += this.cart[i].quantity;
      }
      return tongsl;
    },
    total() {
      var tongtien = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tongtien += this.cart[i].quantity * this.cart[i].price;
      }
      return tongtien;
    },
  },
};
</script>

<style scoped>
GridLayout {
  text-align: center;
}

</style>
