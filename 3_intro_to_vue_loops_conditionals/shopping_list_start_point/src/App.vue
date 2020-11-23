<template>
  <div id="app">
    <form v-on:submit.prevent="saveNewItem">
      <label for="new-item">Add a new item</label>
      <!-- v-model two-way value if I change it in the first place, it affects the second, if I change it in the second place, it affects the first-->
      <input type="text" id="new-item" v-model="newItem">
      <br><label for="purchased">Did you purchase this?</label>
      <select name="isPurchased" id="isPurchased" v-model="isPurchased">
        <option value="true">Yes</option>
        <option value="false">No</option>
      </select>
      <br><input type="submit" value="Click to save a new item">

    </form>
  
    <ul>
      <!-- this makes the items for the list, from 'items'. A quick way, via vue -->
      <!-- check about 50 minutes into recording for conditions on the list display -->
      <!-- The index is crucial, in the for loop, because it needs the index to update the isPurchased value -->
      <!-- the next line is an error until we identify how many list items there will be - v-bind:key="index" -->
      <!-- <li v-for="(item, index) in items" v-bind:key="index"> next bit explains av 'turnery statement' 
      v-bind:class="item.isPurchased ? 'purchased':'not-purchased' " true, do the one on the left, false, do the one on the right -->
      <li v-for="(item, index) in items" v-bind:key="index" v-bind:class="item.isPurchased ? 'purchased':'not-purchased' ">
        <span>{{item.name}}</span>
        <span v-if=item.isPurchased>Purchased</span>
        <!-- this is going to do something after clicking the Purchase button, in a method called buyItem -->
        <button v-if="!item.isPurchased" v-on:click="buyItem(index)">Purchase</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
    return {
      // This will make the list items into objects, they were just ["Milk", "cheese", "beans"]
      items: [
        {name: "Milk", isPurchased: false}, 
        {name: "Cheese", isPurchased: false}, 
        {name: "Beans", isPurchased: true}, 
      ],
      newItem: ""
    }
  },
  methods: {
    saveNewItem: function() {
      this.items.push({
        name: this.newItem,
        isPurchased: "",
      });
      this.newItem = "";
    },
    buyItem: function(index) {
      this.items[index].isPurchased = true;
    }

    // Not needed for Vue
    // handleSubmit: function(event) {
    //   event.presentDefault()
    // }

  }
}
</script>

<style>
#app {
  width: 60%;
  margin: 0 auto;
  font-family: 'Lato', sans-serif;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

li {
  margin: 20px 0;
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

li span {
  padding: 8px;
}

li button {
  background: #f2360c;
  color: #fff;
  border: none;
  padding: 10px;
  cursor: pointer;
}

li.purchased {
  border: 2px solid #1a681e;
  color: #1a681e;
}

li.not-purchased {
  border: 2px solid #f2360c;
}

input[type="text"] {
  padding: 10px;
  width: 50%;
  margin:5px;
}

button, input[type="submit"]{
  padding: 10px;
  background: #000;
  color: #fff;
  cursor: pointer;
  border: 1px solid #000;
}

</style>