<template name="Popup-Item">
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <div class="modal-header__block">
              <h2 class="modal-header__block_title">Set Video Stream</h2>
              <button class="modal-header__block_btn" @click="$emit('close')">
                <i class="fa-solid fa-xmark"></i>
              </button>
            </div>
          </div>

          <div class="modal-body">
            <div class="modal-body__search">
              <label for="search" class="l-search">Search</label>
              <input
                type="text"
                class="i-search"
                id="search"
                v-model="searchFolders"
              />
            </div>

            <div class="modal-body__list-camera">
              <div class="lists scroll">
                <!-- lists header -->
                <div class="lists__header">
                  <div class="lists__header_block" @click="sortName">
                    <div class="sorts">
                      <div class="sort-up"></div>
                      <div class="sort-down"></div>
                    </div>
                    <div class="name">Name</div>
                  </div>
                  <div class="lists__header_block" @click="sortId">
                    <div class="sorts">
                      <div class="sort-up"></div>
                      <div class="sort-down"></div>
                    </div>
                    <div class="name">ID</div>
                  </div>
                </div>
                <!-- end lists header -->

                <!-- folders -->
                <div class="lists__body">
                  <ul class="folders">
                    <li
                      class="folders__item"
                      v-for="(item, index) in searchFolder"
                      :key="index"
                    >
                      <div class="folder">
                        <div class="icon">
                          <i class="fa-solid fa-sort-down"></i>
                          <img
                            src="@/assets/img/bare-metal-server-svgrepo-com.svg"
                            alt="bare-metal-server-svgrepo-com"
                          />
                          <div class="folder-name" @click="openFolder(item)">
                            {{ item.name }}
                          </div>
                        </div>
                        <div class="checkbox">
                          <input type="checkbox" :id="item.id" />
                          <label :for="item.id"></label>
                        </div>
                      </div>

                      <ul class="next_f">
                        <li class="next_f__item" v-if="item.isOpen">
                          <!-- folders -->
                          <div
                            class="folder"
                            v-for="(folder, index) in item.groups"
                            :key="index + folder.name"
                          >
                            <div class="icon">
                              <img
                                src="@/assets/img/security-camera-cctv-svgrepo-com.svg"
                                alt="security-camera-cctv-svgrepo-com"
                                v-if="!isActiveCheck[folder.id]"
                              />
                              <img
                                src="@/assets/img/security-camera-green.svg"
                                alt="security-camera-green"
                                v-else
                              />
                              <p
                                class="folder-name"
                                :class="{ active: isActiveCheck[folder.id] }"
                              >
                                {{ folder.name }}
                              </p>
                            </div>
                            <div class="numb-check">
                              <span class="number">45</span>
                              <div class="checkbox">
                                <input
                                  type="checkbox"
                                  :id="folder.id"
                                  @change="check(folder)"
                                />
                                <label :for="folder.id"></label>
                              </div>
                            </div>
                          </div>
                          <!-- files -->
                          <div
                            class="folder"
                            v-for="(file, index) in item.files"
                            :key="index + file.name"
                          >
                            <div class="icon">
                              <img
                                src="@/assets/img/file-svgrepo-com.svg"
                                alt="file-svgrepo-com"
                              />
                              <p
                                class="folder-name"
                                :class="{
                                  active: isActiveCheckFile[file.id],
                                }"
                              >
                                {{ file.name }}
                              </p>
                            </div>
                            <div class="numb-check">
                              <span class="number">45</span>
                              <div class="checkbox">
                                <input
                                  type="checkbox"
                                  :id="file.id"
                                  @change="checkFile(file)"
                                />
                                <label :for="file.id"></label>
                              </div>
                            </div>
                          </div>
                        </li>
                      </ul>
                    </li>
                  </ul>
                  <!-- end folders -->
                </div>
              </div>

              <!-- images camera -->
              <div class="camera-block">
                <div class="camera">
                  <img src="@/assets/img/img1.png" alt="photo-camera" />
                </div>
                <div class="description">
                  <ul
                    class="description__list"
                    v-for="(item, i) in cameraDesc"
                    :key="i"
                  >
                    <li class="description__list_item left">
                      <p class="text">{{ item.name }}</p>
                    </li>
                    <li class="description__list_item right">
                      <p class="text">
                        {{ item.title }}
                        <span v-html="item.icon">{{ item.icon }}</span>
                      </p>
                    </li>
                  </ul>
                </div>
              </div>
              <!-- end images camera -->
            </div>
          </div>

          <div class="modal-footer">
            <button class="btn">set video stream</button>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "Popup-Item",
  data: () => {
    return {
      cameraDesc: [
        {
          name: "Camera",
          title: "Немиров",
          icon: `<i class="fa-solid fa-location-dot"></i>`,
        },
        { name: "Address", title: "Чубинське, вул яблонева, 12", icon: `` },
        { name: "Timezone", title: "Atlantic/Canary +2", icon: `` },
        { name: "Resolution", title: "500x300", icon: `` },
        { name: "Codec", title: "H264", icon: `` },
        { name: "Type", title: "rtsp", icon: `` },
      ],
      root: [
        {
          id: 15,
          name: "Root",
          isOpen: false,
          groups: [
            {
              id: 21,
              name: "Root_name",
              groups: [],
              files: [],
            },
          ],
          files: [
            {
              id: 13,
              name: "test1",
            },
            {
              id: 8,
              name: "test8",
            },
            {
              id: 11,
              name: "test10",
            },
          ],
        },
        {
          id: 10,
          name: "Group",
          isOpen: false,
          groups: [
            {
              id: 2,
              name: "Group_name",
              groups: [],
              files: [],
            },
          ],
          files: [
            {
              id: 3,
              name: "test1",
            },
          ],
        },
        {
          id: 4,
          name: "Folder_2",
          isOpen: false,
          groups: [
            {
              id: 5,
              name: "Folder_name2",
              groups: [],
              files: [],
            },
            {
              id: 15,
              name: "Folder_name15",
              groups: [],
              files: [],
            },
            {
              id: 25,
              name: "Folder_name",
              groups: [],
              files: [],
            },
          ],
          files: [
            {
              id: 6,
              name: "test2",
            },
          ],
        },
        {
          id: 34,
          name: "AAAA",
          isOpen: false,
          groups: [
            {
              id: 50,
              name: "Folder_name2",
              groups: [],
              files: [],
            },
            {
              id: 35,
              name: "Folder_name15",
              groups: [],
              files: [],
            },
            {
              id: 20,
              name: "Folder_name",
              groups: [],
              files: [],
            },
          ],
          files: [
            {
              id: 26,
              name: "test2",
            },
          ],
        },
      ],
      isActiveCheck: [],
      isActiveCheckFile: [],
      searchFolders: "",
    };
  },
  computed: {
    // search folders and files
    searchFolder() {
      return this.root.filter((elem) => {
        return elem.name
          .toLowerCase()
          .includes(this.searchFolders.toLowerCase());
      });
    },
  },
  methods: {
    check(folder) {
      this.$set(this.isActiveCheck, folder.id, !this.isActiveCheck[folder.id]);
    },
    checkFile(file) {
      this.$set(
        this.isActiveCheckFile,
        file.id,
        !this.isActiveCheckFile[file.id]
      );
    },
    sortName() {
      this.root.sort((a, b) => a.name.localeCompare(b.name));
    },
    sortId() {
      return this.root.sort((a, b) => a.id - b.id);
    },
    openFolder(item) {
      item.isOpen = !item.isOpen;
    },
  },
};
</script>
