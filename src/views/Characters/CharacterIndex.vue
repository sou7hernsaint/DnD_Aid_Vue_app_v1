<template>
  <div class="index">
    <!-- <h1>{{ message }}</h1> -->
    <!-- <h3>{{ "Brian's my hero" }}</h3> -->
    <div class="container">
      <!-- Jumbotron Header -->
      <header class="jumbotron my-4">
        <h1 class="display-3">Welcome back {{ the_User.ufirstname }} !</h1>
        <h3>Here are your current characters:</h3>
        <div class="row">
          <!-- Buttons for All and New Characters -->
          <div class="col-lg-6 col-md-6 mb-4">
            <a class="btn btn-danger btn-lg" href="/characters">See all of your characters!</a>
          </div>
          <div class="col-lg-6 col-md-6 mb-4">
            <a class="btn btn-danger btn-lg" href="/character_create">Create a new character!</a>
          </div>
          <!-- target="_blank" -->
        </div>
      </header>
    </div>
    <div class="container">
      <div class="row">
      <!-- Loop for Index of characters -->
        <div v-for="character in characters" v-bind:key="character.index">
          <!-- <router-link v-bind:to="`/characters/${character.id}`"></router-link> -->
          <div class="col-lg-3 col-md-6 mb-4">
            <div class="card h-100">
              <!-- <img class="background" src="@/assets/Character_Avatars/Blue_Eyes_(Cristi-B).jpg" alt="" /> -->
              <!-- <img class="avatar" src="@/assets/Character_Avatars/Blue_Eyes_(Cristi-B).jpg" alt="" /> -->
              <img class="background" src="@/assets/Imgs/Character_Avatars/Blue_Eyes_(Cristi-B).jpg" alt="" />
              <!-- <img class="background" v-bind:src="character.avatar_img" alt="..." /> -->
              <div class="card-body">
                <h4 class="card-title">
                  {{ character.cfirstname }} {{ character.cmiddlename }} {{ character.clastname }}
                </h4>
                <p class="card-text">
                  {{ character.origin_story }}
                </p>
              </div>
              <div class="card-footer">
                <!-- <a class="btn btn-danger" href="/your_character" v-bind:to="`/characters/${character.id}`" > -->
                <!-- <a class="btn btn-danger" v-bind:href="`/your_character/`+character.id">Stay a'while, n listen!</a> -->
                <a class="btn btn-danger" v-bind:href="`/your_character/${character.id}`">See more!</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <p></p>
    <!-- Bootstrap Modal Button -->
    <!-- <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#character-details"> -->
    <!-- More Info
      </button> -->
    <!-- Old Button for Modal -->
    <!-- <p><button v-on:click="charactersShow(character)">More Info</button></p> -->
    <!-- <img v-bind:src="character.image_url" /> -->
    <!-- Bootstrap Modal -->
    <!-- <div class="modal fade" id="#character-details" tabindex="-1">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Further reading ...</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <p>
              Image URL placeholder
              <input type v-model="characters.imgurl" />
            </p>
            <p>
              Name:
              {{ characters }}
            </p>
            <p>
              Abbreviation:
              {{ characters.abbreviation }}
            </p>
            <p>
              Description:
              {{ characters.desc }}
            </p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div> -->
    <!-- Old Modal -->
    <!-- <dialog id="character-details">
      <form method="dialog">
        <h2>Further reading ...</h2>
        <p>
          Image URL placeholder
          <input type v-model="currentCharacter.imgurl" />
        </p>
        <p>
          Name:
          {{ currentCharacter.cfirstname }}
          {{ currentCharacter.cmiddlename }}
          {{ currentCharacter.clastname }}
        </p>
        <p>
          Abbreviation:
          {{ currentCharacter.abbreviation }}
        </p>
        <p>
          Description:
          {{ currentCharacter.desc }}
        </p>
      </form>
    </dialog> -->

    <div></div>
  </div>
</template>

<style>
.background {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 250px;
  height: 250px;
  border-radius: 25%;
}

.avatar {
  vertical-align: middle;
  position: absolute;
  width: 150px;
  height: 150px;
  border-radius: 25%;
}
/* Button spacing not working ... */
/* .btn {
  padding-left: 0.5 !important;
  padding-right: 0.5 !important;
} */
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to your previously-saved characters page!",
      characters: {},
      characterID: "",
      user_id: "",
      cfirstname: "",
      cmiddlename: "",
      clastname: "",
      raceid: "",
      classid: "",
      alignmentid: "",
      languageid: "",
      inventoryid: "",
      strength: "",
      dexterity: "",
      constitution: "",
      intelligence: "",
      wisdom: "",
      charisma: "",
      healthmax: "",
      healthcurrent: "",
      healthtemp: "",
      speed: "",
      origin_story: "",
      currentCharacter: [],
      the_User: [],
    };
  },
  created: function () {
    console.log("Fetching all the characters automatically ...");
    this.charactersIndex();
    // I got this right, except I console.logged it rather than running it as a method
    console.log("Getting your profile info automatically ...");
    // Get request for current_user's info
    this.theUser();
  },
  methods: {
    charactersIndex: function () {
      console.log("charactersIndex action is executing ...");
      // axios.get("http://localhost:3000/api/characters/").then((response) => {
      axios.get("https://dnd-aid-back-end.herokuapp.com/api/characters/").then((response) => {
        // console.log("Here's the data from our personal database ...");
        // console.log(response.data);
        this.characters = response.data;
        // Our table data is entered into the hash of our var "characters"
        console.log("Here's what's in characters:");
        console.log(this.characters);
      });
      // Fetch DnD's table
      // axios.get("https://www.dnd5eapi.co/api/characters/").then((response) => {
      //   console.log("Here's the data from dnd5eapi ...");
      //   console.log(response.data);
      //   this.charactersTheirs = response.data;
      // });
    },
    theUser: function () {
      // axios.get("/api/users/current_user").then((response) => {
      axios.get("https://dnd-aid-back-end.herokuapp.com/api/users/current_user").then((response) => {
        console.log(response.data);
        // current_user's info is stored in var currentUser
        this.the_User = response.data;
      });
    },
    charactersShow: function (theCharacter) {
      console.log("CharactersShow action is executing ...");
      console.log(theCharacter);
      this.currentCharacter = theCharacter;
      // document.querySelector("#character-details").showModal();
      // console.log(this.currentCharacter);
    },
    // characterUpdate: function (theCharacter) {
    //   console.log("Let's change stuff about that character!");
    //   console.log(theCharacter);
    //   var params = {
    //     userid: @theCharacter.userid,
    //     cfirstname: @theCharacter.cfirstname,
    //     cmiddlename: @theCharacter.cmiddlename,
    //     clastname: @theCharacter.clastname,
    //     raceid: @theCharacter.raceid,
    //     classid: @theCharacter.classid,
    //     alignmentid: @theCharacter.alignmentid,
    //     languageid: @theCharacter.languageid,
    //     inventoryid: @theCharacter.inventoryid,
    //     strength: @theCharacter.strength,
    //     dexterity: @theCharacter.dexterity,
    //     constitution: @theCharacter.constitution,
    //     intelligence: @theCharacter.intelligence,
    //     wisdom: @theCharacter.wisdom,
    //     charisma: @theCharacter.charisma,
    //     healthmax: @theCharacter.healthmax,
    //     healthcurrent: @theCharacter.healthcurrent,
    //     healthtemp: @theCharacter.healthtemp,
    //     speed: @theCharacter.speed
    //   },
    //   axios.patch("/api/recipes/" + theProduct.id, params).then((response) => {
    //     console.log(response.data);
    //   }),
  },
};
</script>
