<template>
  <div>
    <div
      v-for="person in peoples"
      :key="person.id"
      style="
        flex: 1 1 33.333%;
        width: 300px;
        padding: 25px;
        display: inline-block;
      "
    >
      <div :class="'list-inner'">
        <div class="list-image-wrap">
          <img :src="person.src" class="image" />
        </div>
        <div>
          <button
            class="OpenModal"
            id="show-modal"
            @click="showModalUser(person)"
          >
            Info
          </button>
        </div>
      </div>
    </div>

    <PModal v-show="showModal" @close="closeModalUser" :person="person">

      <template v-slot:footer>
        <button class="OpenModalChild" @click="showModalChild(person)">
          Detail
        </button>
      </template>
    </PModal>
    <ChildModal v-show="showModal1" @close="closeModalChild" :person="person">
      <template v-slot:header> </template>

      <template v-slot:body> </template>

      <template v-slot:footer> </template>
    </ChildModal>
  </div>
</template>

<script>
import PModal from "../components/PModal.vue";
import ChildModal from "./ChildModal.vue";
export default {
  name: "HelloWorld",
  components: {
    PModal,
    ChildModal,
  },
  data() {
    return {
      showModal: false,
      showModal1: false,
      renderList: [],
      history: [],
      peoples: [
        {
          id: 1,
          name: "Nike",
          counter: 0,
          src: "https://i.pinimg.com/236x/e5/cf/66/e5cf66cf4afaf85d092b9f02509e440e.jpg",
          context:"Are you sure about that?"

        },
        {
          id: 2,
          name: "Nikel",
          src: "https://www.dogalize.com/wp-content/uploads/2017/05/funny-cat-img-200x200.jpg",
          context:"Are you sure about that?"
        },
        {
          id: 3,
          name: "Runs",
          src: "https://i.pinimg.com/474x/02/34/bd/0234bd2da5a29016c7f82e8fa5669781.jpg",
          context:"Are you sure about that?"

        },
        {
          id: 4,
          name: "Nikex",
          src: "https://i.pinimg.com/originals/a9/39/52/a93952379d9b4f44e413df0118e57b1b.jpg",
          context:"Are you sure about that?"
        },
        {
          id: 5,
          name: "Sux",
          src: "https://i.pinimg.com/originals/00/d7/59/00d759aeb06c81fff12790b8ddacc50a.jpg",
          context:"Are you sure about that?"
        },
      ],
    };
  },
  created() {
    this.renderList = Object.assign([], this.peoples);

  },
  watch: {
    peoples: {
      handler() {
      },
      deep: true,
    },
  },
  methods: {
    showModalUser(value) {
      this.showModal = true;
      this.person = value;
    },
    closeModalUser() {
      this.showModal = false;
    },
    
    showModalChild(value) {
      this.showModal1 = true;
      this.person = value;
    },
    closeModalChild() {
      this.showModal1 = false;
    },
    onVote(data) {
      this.topRank(), this.history.push(data);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>
.list-inner {
  position: relative;
  padding: 25px;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  perspective: 1000px;
}

.list-image-wrap {
  position: relative;
  z-index: 1;
  transform-origin: center;
}

.list-image-wrap .image {
  width: 100%;
  filter: drop-shadow(0px 0px 12px rgba(0, 0, 0, 0.25));
}



img {
  width: 75%;
  height: auto;
  border-radius: 5px;
}
.OpenModal {
  border: none;
  outline: 0;
  padding: 12px;
  color: black;
  background-color: green;
  text-align: center;
  cursor: pointer;
  width: 70%;
  font-size: 18px;
}
.OpenModal:hover {
  background-color: rgb(255, 0, 0);
}
.OpenModalChild {
  border: none;
  outline: 0;
  padding: 12px;
  margin-bottom: 5px;
  color: white;
  background-color: rgb(57, 223, 168);
  text-align: center;
  cursor: pointer;
  width: 100%;
  font-size: 18px;
}
.OpenModalChild:hover {
  background-color: rgb(19, 145, 103);
}
</style>
