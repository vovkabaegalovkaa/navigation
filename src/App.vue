<template>
  <div class="container">
    <h2>Как сделать яичницу</h2>
    <p class="header">{{ getHeader }}</p>
    <div class="navigationInterface">
      <p class="content">{{ getContent }}</p>
      <div class="navigationBar">
        <span class="navigationItem" :class="getClasses(item)" v-for="item in steps" :key="item.id">{{ item.id }}</span>
      </div>
      <div class="navigationButtons">
        <button class="back button" :disabled="selectedEl == 1 ? true : false" @click="delOne">{{ btnInfo }}</button>
        <button class="button next" v-if="selectedEl != steps.length" @click="addOne">Вперед</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return {
      steps: [
        {
          id: 1,
          header: "Подготовка",
          content: "Подготовьте нужные ингредиенты: 2-3 яйца, соль и перец по вкусу, 1-2 столовые ложки молока или воды (по желанию), масло или оливковое масло для жарки, дополнительные ингредиенты по вашему вкусу (сыр, овощи, ветчина и т.д.)",
        },
        {
          id: 2,
          header: "Яйца",
          content: "Разбейте яйца в миску и добавьте щепотку соли и перца. Если хотите, добавьте молоко или воду для более воздушной текстуры. Взбейте смесь вилкой или венчиком до однородности.",
        },
        {
          id: 3,
          header: "Сковорода",
          content: "Разогрейте сковороду на среднем огне. Добавьте немного масла или оливкового масла и дайте ему полностью разогреться.",
        },
        {
          id: 4,
          header: "Готовка",
          content: "Влейте яичную смесь на разогретую сковороду. Дайте ей немного схватиться, затем аккуратно поднимайте края омлета лопаткой, позволяя жидкой части стекать на дно сковороды. Продолжайте готовить, пока омлет не станет почти полностью твердым.",
        },
        {
          id: 5,
          header: "Подача",
          content: "Когда омлет почти готов, добавьте на одну половину омлета выбранную начинку (сыр, овощи...",
        }
      ],
      selectedEl: 1,
      isSelectedElLast: false,
      btnInfo: "Назад"
    }
  },
  methods: {
    getClasses(item){
      let classes = [];
      if(item.id == this.selectedEl){
        classes.push("selected");
      }
      if(item.id < this.selectedEl){
        classes.push("accepted");
      }
      return classes;
    },
    addOne(){
      this.selectedEl++;
      if(this.selectedEl == this.steps.length){
        this.isSelectedElLast = true;
      }
    },
    delOne(){
      if(this.isSelectedElLast){
        this.selectedEl = 1;
        this.isSelectedElLast = false;
        return
      }
      else{
        this.selectedEl--;
      }
    }
  },
  computed: {
    getHeader(){
      return this.steps[this.selectedEl - 1].header;
    },
    getContent(){
      return this.steps[this.selectedEl - 1].content;
    },
  },
  watch: {
    isSelectedElLast(value){
      if(value){
        this.btnInfo = "Заново";
      }
      else{
        this.btnInfo = "Назад";
      }
    }
  }
}
</script>

