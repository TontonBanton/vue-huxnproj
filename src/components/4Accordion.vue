<template>
  <h2>Accordion</h2>
  <h3 style="font-size: 1rem;">Takeways: array.map(), ...spreadoperator, ifelseshorthand value: (condition) ? true:false </h3>

  <div class="accordion-container">
    <div v-for="(item, keyIndex) in items" :key="keyIndex" class="accordion">
      <div class="accordion-header" @click="toggleAccordion(keyIndex)">
        {{ item.title }}
        <span class="arrow-icon">{{ item.open ? "🔻" : "▶"}}</span>
      </div>
      <div v-show="item.open" class="accordion-content">
        {{ item.content }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const items = ref([
  {
    title: "What is HTML?",
    content:
      "The HyperText Markup Language or HTML is the standard markup language for documents designed to be displayed in a web browser. It defines the content and structure of web content. It is often assisted by technologies such as Cascading Style Sheets and scripting languages such as JavaScript.",
    open: false,
  },
  {
    title: "What is CSS?",
    content:
      "Cascading Style Sheets is a style sheet language used for specifying the presentation and styling of a document written in a markup language such as HTML or XML. CSS is a cornerstone technology of the World Wide Web, alongside HTML and JavaScript.",
    open: false,
  },
  {
    title: "What is JS?",
    content:
      "JavaScript, often abbreviated as JS, is a programming language and core technology of the World Wide Web, alongside HTML and CSS. As of 2023, 98.7% of websites use JavaScript on the client side for webpage behavior, often incorporating third-party libraries.",
    open: false,
  },
]);

//Implicit Return
const toggleAccordion = (fromKeyIndex)=> {
  items.value = items.value.map((item,arrayIndex)=> ({            // Create a new array by mapping over each item in the original items array
    ...item,                                                      //spread operator - create item object with all its properties in the array
    open: (arrayIndex === fromKeyIndex) ? !item.open : false      //shorthand ifelse - change the value of item.open if arrayindex and keyindex are the same
  }))
}

/* Beginner Explicit Return
const toggleAccordionV1 = (fromKeyIndex) => {
  items.value = items.value.map((item, arrayIndex) => {           // Create a new array by mapping over each item in the original items array
    let newItem = { ...item };                                    // Create a new object with all the properties of the current item
    if (arrayIndex === fromKeyIndex) {                            // Check if the current index matches the index passed to the function
      newItem.open = !item.open;                                  // Toggle the "open" property of the item (true becomes false, false becomes true)
    } else {
      newItem.open = false;                                       // Ensure the "open" property is set to false for all other items
    }
    return newItem;                                                // Return the updated item
  });
}
*/

</script>
<style scoped>
.accordion-container {
  max-width: 600px;
  margin: 50px auto;
}
.accordion {
  border: 1px solid #ddd;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 10px;
}
.accordion-header {
  background-color: #3498db;
  color: #fff;
  padding: 15px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.arrow-icon {
  font-size: 20px;
}
.accordion-content {
  padding: 15px;
  display: none;
  border-top: 1px solid #ddd;
  background-color: #f9f9f9;
  color: #333;
}
.accordion-content[style] {
  display: block;
}
</style>