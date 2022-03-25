<template>
    <div class="container mx-auto">
        <div
        class="py-8 border-b border-gray-500"
        v-for="object of objects"
        :key="object.id"
        >
        <p class="font-bold text-xl">{{object.id}}. {{object.title}}</p>       
        <p class="font-bold text-xl">{{object.desc}}</p>   
        </div>

        <form class="block my-10" action="">
        <p class="text-xl font-bold">Enter title:</p>
        <input
            class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
            type="text"
            v-model="form.title"
            placeholder="Enter title..."
        />
        <p class="text-xl font-bold">Enter description:</p>
        <input
            class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
            type="text"
            v-model="form.desc"
            placeholder="Enter desc..."
        />
        <button
            class="
            bg-green-400
            px-20
            py-4
            text-white
            mx-auto
            block
            rounded-xl
            font-bold
            text-2xl
            "
            @click="addObject()"
        >
            Add Object
        </button>
        </form>
    </div>

</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      objects: [],
      baseURL: "http://localhost:3001/objects",
      form: {
        title: "",
        desc: "",
      },
    };
  },
  async created() {
    try {
      const res = await axios.get(this.baseURL);
      this.objects = res.data;
    } catch (e) {
      console.error(e);
    }
  },  
  methods: {
    async addObject() {
      try {
        const res = await axios.post(this.baseURL, {
          title: this.form.title,
          desc: this.form.desc,
        });
        this.objects = [...this.objects, res.data];
      } catch (e) {
        console.error(e);
      }
    },
  },
};
</script>