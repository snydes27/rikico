<template>
<div>
  <h1>Scraps</h1>
    <div class="container-fluid">
    <b-input-group size="sm" class="mb-2">
      <b-input-group-prepend is-text>
        <b-icon icon="search"></b-icon>
      </b-input-group-prepend>
      <b-form-input type="search" placeholder="Search scraps" v-model="search"></b-form-input>
    </b-input-group>

    <b-card-group columns>
      <b-card
        v-for="scrap in scraps"
        v-bind:key="scrap.id"
        class="line-break"
      >
        <div>{{ scrap.scrapBody }}</div>
        
        <div class="d-flex justify-content-between">
          <b-badge variant="primary">
            {{ scrap.tag }}
          </b-badge>

          <b-button @click="editScrap()" size="sm" variant="outline">
            <b-icon icon="pencil"></b-icon>
          </b-button>
        </div>
        
      </b-card>
    </b-card-group>

  <div>
    <b-modal ref="add-scrap-modal" id="add-scrap-modal" size="lg" ok-title="Save" no-close-on-backdrop hide-footer title="Add Scrap">
      <b-form @submit.prevent="saveScrap">
        <div class="container">
          <div class="row justify-content-center">
            <div class="col-lg-12">
              <div class="card bg-light">
                <div class="card-body">
                  <section class="form-group">
                    <label class="form-control-label sr-only" for="Email">Title</label>
                    <input
                      placeholder="Title"
                      class="form-control"
                      type="text"
                      v-model="scrap.title"
                    />
                  </section>
                  <b-form-textarea class="mb-2"
                    id="textarea-auto-height"
                    placeholder="Enter Your Scrap"
                    size="sm"
                    rows="4"
                    v-model="scrap.scrapBody"
                    max-rows="8"
                    autofocus="true">
                    
                  </b-form-textarea>
                  <div>
                    <b-form-tags
                      input-id="tags-pills"
                      tag-variant="primary"
                      tag-pills
                      size="sm"
                      separator=" "
                      placeholder="Enter new tags separated by space"
                      class="mb-2"
                      v-model="scrap.tag"
                      name="tag"
                    ></b-form-tags>
                  </div>
                  <div class="form-group text-right mb-0">
                    <button class="btn btn-primary" type="submit">Save</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>  
      </b-form>
    </b-modal>
  </div>

<div>
    <b-modal ref="edit-scrap-modal" id="edit-scrap-modal" size="lg" ok-title="Save" no-close-on-backdrop hide-footer title="Add Scrap">
      <b-form @submit.prevent="editScrap">
        <div class="container">
          <div class="row justify-content-center">
            <div class="col-lg-12">
              <div class="card bg-light">
                <div class="card-body">
                  <section class="form-group">
                    <label class="form-control-label sr-only" for="Email">Title</label>
                    <input
                      placeholder="Title"
                      class="form-control"
                      type="text"
                      v-model="scrap.title"
                    />
                  </section>
                  <b-form-textarea class="mb-2"
                    id="textarea-auto-height"
                    placeholder="Enter Your Scrap"
                    size="sm"
                    rows="4"
                    v-model="scrap.scrapBody"
                    max-rows="8"
                    autofocus="true">
                    
                  </b-form-textarea>
                  <div>
                    <b-form-tags
                      input-id="tags-pills"
                      tag-variant="primary"
                      tag-pills
                      size="sm"
                      separator=" "
                      placeholder="Enter new tags separated by space"
                      class="mb-2"
                      v-model="scrap.tag"
                      name="tag"
                    ></b-form-tags>
                  </div>
                  <div class="form-group text-right mb-0">
                    <button class="btn btn-primary" type="submit">Save</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>  
      </b-form>
    </b-modal>
  </div>

  </div>
  <b-button @click="addScrap()" pill size="lg" variant="outline-secondary">
    <b-icon icon="plus" class=""></b-icon>
  </b-button>

</div>

</template> 


<script>
export default {
  name: "Scraps",
  props: ["user", "scraps"],

  data: function() {
    return {
      scrap: {
        title: null,
        scrapBody: null,
        tag: null,
        recorded: null,
      },
      
      search: ""
    };
  },
  methods: {
    addScrap() {
      this.$refs['add-scrap-modal'].show()
    },
    editScrap: function() {
      this.$emit("saveScrap", this.scrap);
        this.scrap.title = null;
        this.scrap.scrapBody = null;
        this.scrap.tag = null;
    },
    saveScrap: function() {
      this.$emit("saveScrap", this.scrap);
        this.scrap.title = null;
        this.scrap.scrapBody = null;
        this.scrap.tag = null;
    },
    
  },
  computed: {
    filteredScraps: function() {
      //const dataFilter = item => item.scrapBody.toLowerCase().match(this.search.toLowerCase()) && true;
      //return this.scrapSearch.filer(dataFilter);
      
      return this.scraps.filter((scrap) => {
        return scrap.scrapBody.toLowerCase().match(this.search.toLowerCase());
      });
    }
  }
}


</script>


<style scoped>

/* Keeps the line break for the cards */
.line-break {
  white-space: pre-line;
}

.badge {
  padding-bottom: 1px;
  font-size: 11px;
  margin-top: 8px;
}

.btn .btn-outline .btn-sm  {
  margin: 1px;
}

.edit-scrap {
  
}

.badge-primary {
    color: #f8f9fa;
    background-color: #91B6BF;
}

#textarea-auto-height {
  overflow: hidden !important;
}

/*Action button*/
.rounded-pill {
  display: inline-flex;
	align-items: center;
	justify-content: center;
	position: fixed;
	right: 50px;
	bottom: 50px;
	user-select: none;
  border-radius: 50%;
  font-size: 24px;
  line-height: 1.33;
  z-index: 1;
  width: 70px;
  height: 70px;
  cursor: pointer; 
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.19), 0 4px 4px rgba(0, 0, 0, 0.23);

}

.container-fluid {
 
}

.card-body {
  padding: 6px;
  font-size: 13px;
}


</style>