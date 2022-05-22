<script setup lang="ts">
import { reactive } from "vue";
import { supabase } from "../supabase";
import Swal from "sweetalert2";

const survey = reactive({
  fullname: "",
  class: "",
  course: "",
});

const clearForm = () => {
  survey.fullname = "";
  survey.class = "";
  survey.course = "";
};

const submitData = async () => {
  try {
    const { error } = await supabase.from("survey").insert([
      {
        fullname: survey.fullname,
        class: survey.class,
        course: survey.course,
      },
    ]);
    clearForm();
    if (error) throw error;
    Swal.fire("Terimakasih", "Terimakasih atas Partisipasi nya", "success");
  } catch (error: any) {
    console.log(error);
    Swal.fire("Error :(", `${error.message}`, "error");
  }
};
</script>
<template>
  <div class="w-full max-w-xs">
    <form
      @submit.prevent="submitData()"
      class="bg-white shadow-xl border-3 border-gray-200 rounded px-8 pt-6 pb-8 mb-4"
    >
      <div class="mb-4">
        <label
          class="block text-gray-700 text-sm font-bold mb-2"
          for="fullname"
        >
          Nama Lengkap
        </label>
        <input
          v-model="survey.fullname"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          placeholder="Fahmi Sugiarto"
        />
      </div>
      <div class="mb-4">
        <label
          class="block text-gray-700 text-sm font-bold mb-2"
          for="fullname"
        >
          Course
        </label>
        <div class="flex flex-col gap-y-4">
          <div class="form-check">
            <input
              v-model="survey.course"
              class="form-check-input appearance-none rounded-full h-4 w-4 border border-gray-300 bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 mt-1 align-top bg-no-repeat bg-center bg-contain float-left mr-2 cursor-pointer"
              type="radio"
              value="WP"
            />
            <label
              class="form-check-label inline-block text-gray-800"
              for="flexRadioDefault1"
            >
              Web Programing
            </label>
          </div>
          <div class="form-check">
            <input
              v-model="survey.course"
              class="form-check-input appearance-none rounded-full h-4 w-4 border border-gray-300 bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 mt-1 align-top bg-no-repeat bg-center bg-contain float-left mr-2 cursor-pointer"
              type="radio"
              name="flexRadioDefault"
              value="UI/UX"
            />
            <label
              class="form-check-label inline-block text-gray-800"
              for="flexRadioDefault1"
            >
              UI/UX
            </label>
          </div>
          <div class="form-check">
            <input
              v-model="survey.course"
              class="form-check-input appearance-none rounded-full h-4 w-4 border border-gray-300 bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 mt-1 align-top bg-no-repeat bg-center bg-contain float-left mr-2 cursor-pointer"
              type="radio"
              name="flexRadioDefault"
              value="SO"
            />
            <label
              class="form-check-label inline-block text-gray-800"
              for="flexRadioDefault1"
            >
              Sistem Operasi
            </label>
          </div>
          <div class="form-check">
            <input
              v-model="survey.course"
              class="form-check-input appearance-none rounded-full h-4 w-4 border border-gray-300 bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 mt-1 align-top bg-no-repeat bg-center bg-contain float-left mr-2 cursor-pointer"
              type="radio"
              name="flexRadioDefault"
              value="AP"
            />
            <label
              class="form-check-label inline-block text-gray-800"
              for="flexRadioDefault1"
            >
              Algoritma Pemograman
            </label>
          </div>
        </div>
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="kelas">
          Kelas
        </label>
        <input
          v-model="survey.class"
          class="shadow appearance-none rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          placeholder="A1"
        />
      </div>
      <div class="flex items-center justify-between">
        <button
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
          type="submit"
        >
          Submit
        </button>
      </div>
    </form>
    <p class="text-center text-gray-500 text-xs">
      &copy;2022 by Fahmi. All rights reserved.
    </p>
  </div>
</template>
