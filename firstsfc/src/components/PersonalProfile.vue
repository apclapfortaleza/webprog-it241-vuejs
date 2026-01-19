<template>
    <canvas id="particle-canvas"></canvas>
    <div class="cursor-shadow"></div>

    <nav class="navbar navbar-expand-lg navbar-light bg-white shadow-sm sticky-top">
      <div class="container">
        <button class="navbar-toggler ms-auto" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item"><a class="nav-link" href="#about">Who</a></li>
            <li class="nav-item"><a class="nav-link" href="#edu">Education</a></li>
            <li class="nav-item"><a class="nav-link" href="#exp">Portfolio</a></li>
            <li class="nav-item"><a class="nav-link" href="#hobbies">Hobbies</a></li>
            <li class="nav-item"><a class="nav-link" href="#memory-heart">Gallery</a></li>
            <li class="nav-item"><a class="nav-link" href="#guestbook">Guestbook</a></li>
            <li class="nav-item"><a class="nav-link" href="#resources">Resources</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <main class="stack-wrapper">
      <section class="content-section" id="about">
        <div class="container h-100 d-flex align-items-center">
          <div class="row align-items-center w-100 flex-column-reverse flex-lg-row">
            <div class="col-lg-7 about text-center text-lg-start mt-5 mt-lg-0">
              <h1 class="display-2 fw-bold">Hello! I'm Lance Art</h1>
              <p class="lead ms-lg-3">My name is Lance Art P. Fortaleza and I am an inspiring full-stack developer!</p>
              <div class="social-links ms-lg-3 d-flex justify-content-center justify-content-lg-start gap-3">
                <a href="https://github.com/apclapfortaleza"><i class="fa-brands fa-github"></i></a>
                <a href="https://www.linkedin.com/in/lance-art-fortaleza-47299b321"><i class="fa-brands fa-linkedin"></i></a>
                <a href="https://www.facebook.com/boszlance23/"><i class="fa-brands fa-facebook"></i></a>
                <a href="https://www.instagram.com/lnzlart/"><i class="fa-brands fa-instagram"></i></a>
              </div>
            </div>
            <div class="col-lg-5 d-flex justify-content-center position-relative">
              <div class="profile-circle"></div>
            </div>
          </div>
        </div>
      </section>

      <section class="content-section bg-light border-top border-bottom" id="edu">
        <div class="container h-100 d-flex align-items-center">
          <div class="row w-100 align-items-center">
            <div class="col-lg-5 d-flex justify-content-center mb-4 mb-lg-0">
              <div class="edu-image-wrapper">
                <img v-bind:src="activeEduImage" src="./css/assets/apc.jpg" id="edu-display-img" class="img-fluid rounded shadow-lg" alt="Education">
              </div>
            </div>
            <div class="col-lg-7 text-center text-lg-start">
              <div class="d-flex align-items-center justify-content-center justify-content-lg-start mb-4">
                <h2 class="display-3 fw-bold mb-0">Education</h2>
                <img src="https://media0.giphy.com/media/v1.Y2lkPTZjMDliOTUycXJrNm94MnRqN2t3aDdybGZ4OHV1ZHRuYThtc3Vtb3JjYWx1NmN0ZyZlcD12MV9zdGlja2Vyc19zZWFyY2gmY3Q9cw/C0L6c8KLHAiY0/200w.gif" alt="icon" class="header-gif ms-3" style="width: 50px;">
              </div>
              <ul class="list-unstyled custom-list">
                <li class="mb-3" v-on:mouseenter="changeEduImage('./css/assets/apc.jpg')">
                  <i class="fas fa-university me-2"></i> Currently taking <strong>Bachelor of Information Technology</strong> at Asia Pacific College
                </li>
                <li class="mb-3" v-on:mouseenter="changeEduImage('./css/assets/sti.jpg')">
                  <i class="fas fa-code me-2"></i> Senior Highschool <strong>'Mobile App & Web Development'</strong> graduate at STI Pasay-EDSA
                </li>
                <li class="mb-3" v-on:mouseenter="changeEduImage('./css/assets/apec.jpg')">
                  <i class="fas fa-graduation-cap me-2"></i> Highschool graduate at APEC Schools Roxas.
                </li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <section class="content-section" id="exp">
        <div class="blob-container">
          <div class="blob"></div>
          <div class="blob"></div>
          <div class="blob"></div>
        </div>
        <div class="container h-100 d-flex flex-column justify-content-start pt-5">
          <div class="exp-layout-wrapper w-100 text-center" v-bind:class="{'show-details': activeProject}">
            <div class="portfolio-header mb-5">
              <h2 class="display-3 fw-bold mb-0">Portfolio</h2>
            </div>
            <div class="exp-content-body d-flex flex-column align-items-center">
              <div class="exp-icons-container d-flex flex-row justify-content-center flex-wrap gap-4 mb-5">
                <div v-for="project in projects" v-bind:key="project.id" class="exp-item" v-bind:class="{ active: activeProject && activeProject.id === project.id }" v-on:mouseenter="selectProject(project)" v-on:click="selectProject(project)">
                  <img v-bind:src="project.image" v-bind:alt="project.title" class="rounded shadow-sm">
                </div>
              </div>
              <div class="exp-details-panel w-100" v-if="activeProject">
                <div class="details-content mx-auto" v-bind:key="activeProject.id">
                  <h2 class="display-5 fw-bold">{{ activeProject.title }}</h2>
                  <p class="lead text-muted">{{ activeProject.subtitle }}</p>
                  <p class="lead mb-4">{{ activeProject.desc }}</p>
                  <div class="project-media-gallery mt-4">
                    <template v-if="activeProject.media && activeProject.media.length > 1">
                      <div v-bind:id="'projectCarousel-' + activeProject.id" class="carousel slide mx-auto" data-bs-ride="false" style="max-width: 800px;">
                        <div class="carousel-inner shadow-lg rounded">
                          <div v-for="(item, index) in activeProject.media" v-bind:key="index" v-bind:class="['carousel-item', { 'active': index === 0 }]">
                            <div class="media-wrapper">
                              <template v-if="item.type === 'image'">
                                <img v-bind:src="item.src" v-bind:alt="item.alt" class="d-block w-100" loading="lazy">
                              </template>
                              <template v-else-if="item.type === 'youtube'">
                                <div class="ratio ratio-16x9">
                                  <iframe v-bind:src="item.src" title="YouTube video" allowfullscreen></iframe>
                                </div>
                              </template>
                              <template v-else-if="item.type === 'video'">
                                <video controls class="w-100 rounded">
                                  <source v-bind:src="item.src" type="video/mp4">
                                </video>
                              </template>
                            </div>
                          </div>
                        </div>
                        <button class="carousel-control-prev" type="button" v-bind:data-bs-target="'#projectCarousel-' + activeProject.id" data-bs-slide="prev">
                          <span class="carousel-control-prev-icon"></span>
                        </button>
                        <button class="carousel-control-next" type="button" v-bind:data-bs-target="'#projectCarousel-' + activeProject.id" data-bs-slide="next">
                          <span class="carousel-control-next-icon"></span>
                        </button>
                      </div>
                    </template>
                    <template v-else-if="activeProject.media && activeProject.media.length === 1">
                      <div class="media-wrapper mx-auto shadow-lg rounded" style="max-width: 800px;">
                        <img v-if="activeProject.media[0].type === 'image'" v-bind:src="activeProject.media[0].src" class="img-fluid rounded" alt="Project detail">
                        <video v-else-if="activeProject.media[0].type === 'video'" controls class="w-100 rounded">
                          <source v-bind:src="activeProject.media[0].src" type="video/mp4">
                        </video>
                      </div>
                    </template>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section v-bind:class="['content-section', 'hobby-bg-transition', 'hobby-bg-' + activeHobby]" id="hobbies">
        <div class="container h-100 d-flex flex-column justify-content-center py-5">
          <h2 class="display-3 fw-bold text-center mb-5 text-white">Hobbies & Interests</h2>
          <div class="hobby-nav d-flex justify-content-center gap-3 mb-5">
            <button v-for="(hobby, key) in hobbyData" v-bind:key="key" v-on:click="handleHobbyChange(key)" v-bind:class="['btn-hobby', { active: activeHobby === key }]">
              <i v-bind:class="hobby.icon"></i> {{ hobby.title }}
            </button>
          </div>
          <div class="hobby-stage shadow-lg" style="overflow: visible !important;">
            <transition name="hobby-fade" mode="out-in">
              <div v-if="activeHobby === 'music'" key="music" class="music-player-zone text-center w-100">
                <div class="player-container d-flex flex-column align-items-center">
                  <div v-bind:class="['cd-slot', { 'has-cd': selectedCD }]">
                    <div v-if="selectedCD" class="spinning-cd" v-bind:style="{ backgroundImage: 'url(' + selectedCD.img + ')', animationDuration: rotationSpeed }">
                      <div class="cd-label"></div>
                    </div>
                    <div v-else class="cd-placeholder">
                      <i class="fas fa-compact-disc fa-5x text-secondary"></i>
                      <p class="text-secondary mt-2">Select a CD</p>
                    </div>
                  </div>
                  <div class="controls mt-4 w-100" style="max-width: 400px;">
                    <div v-if="selectedCD">
                      <div class="marquee-wrapper mx-auto mt-3" style="width: 200px;">
                        <div class="marquee-container">
                          <span class="scrolling-text">{{ selectedCD.name }} - {{ selectedCD.artist }}</span>
                        </div>
                        <div class="progress-container" v-on:click="seekAudio">
                          <div class="progress-bar" v-bind:style="{ width: audioProgress + '%' }"></div>
                        </div>
                      </div>
                      <div class="custom-player d-flex justify-content-center align-items-center gap-3 mt-4">
                        <button class="player-btn" v-on:click="restartAudio"><i class="fas fa-backward-step"></i></button>
                        <button class="player-btn play-pause-btn" v-on:click="togglePlay">
                          <i v-bind:class="isPlaying ? 'fas fa-circle-pause' : 'fas fa-circle-play'"></i>
                        </button>
                        <div class="d-flex align-items-center gap-2 ms-2 ps-2 border-start border-white border-opacity-10">
                          <button class="player-btn" v-on:click="toggleMute">
                            <i v-bind:class="isMuted ? 'fas fa-volume-xmark' : 'fas fa-volume-high'"></i>
                          </button>
                          <input type="range" class="volume-slider" min="0" max="1" step="0.1" v-model="audioVolume" v-on:input="setVolume" style="width: 80px;">
                        </div>
                      </div>
                    </div>
                    <div class="cd-rack-grid mt-5">
                      <div v-for="cd in hobbyData.music.top5" v-bind:key="cd.name" class="cd-case" v-on:click="playCD(cd)">
                        <div class="jewel-case">
                          <img v-bind:src="cd.img" v-bind:alt="cd.name" class="album-art img-fluid rounded">
                        </div>
                        <p class="small text-center mt-2 text-white fw-bold">{{ cd.name }}</p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div v-else-if="activeHobby === 'games'" key="games" class="games-zone w-100">
                <div class="device-container">
                  <div v-bind:class="['device-frame', hobbyData.games.selectedGame?.device || 'pc']">
                    <div v-if="hobbyData.games.selectedGame?.device === 'mobile'" class="device-notch"></div>
                    <div class="game-screen" v-bind:style="{ backgroundColor: hobbyData.games.selectedGame?.color || '#000' }">
                      <div v-if="hobbyData.games.selectedGame" class="game-content">
                        <img v-bind:src="hobbyData.games.selectedGame.icon" class="game-logo-large" alt="Game Logo">
                        <h4 class="mt-2 arcade-font">{{ hobbyData.games.selectedGame.name }}</h4>
                      </div>
                      <div v-else class="pc-idle">
                        <i class="fas fa-power-off text-muted mb-2"></i>
                        <p class="small text-muted">Awaiting Input...</p>
                      </div>
                    </div>
                  </div>
                  <div class="monitor-support" v-if="!hobbyData.games.selectedGame || hobbyData.games.selectedGame.device === 'pc'">
                    <div class="stand-neck"></div>
                    <div class="stand-base"></div>
                  </div>
                </div>
                <div class="game-library d-flex justify-content-center gap-3 mt-4">
                  <div v-for="game in hobbyData.games.items" v-bind:key="game.name" class="game-card" v-bind:class="{ active: hobbyData.games.selectedGame?.name === game.name }" v-on:click="hobbyData.games.selectedGame = game">
                    <img v-bind:src="game.icon" class="game-mini-icon" alt="Game Icon">
                  </div>
                </div>
              </div>
              <div v-else key="default" class="misc-zone text-center w-100">
                <h3 class="mb-4">{{ hobbyData[activeHobby].title }}</h3>
                <ul class="list-unstyled lead hobby-list">
                  <li v-for="item in hobbyData[activeHobby].items" v-bind:key="item" class="mb-3 bop-text">
                    <i class="fas fa-check-circle text-primary me-2"></i> {{ item }}
                  </li>
                </ul>
              </div>
            </transition>
          </div>
        </div>
      </section>

      <section id="memory-heart" class="content-section mt-5 py-5 position-relative">
        <div class="heart-bg-container">
          <img src="https://media.tenor.com/QReB8xWJvRsAAAAi/heart.gif" class="heart-gif-under" alt="heart background">
        </div>
        <div class="container text-center position-relative" style="z-index: 2;">
          <h2 class="arcade-font mb-4 gallery-title"><i class="fas fa-heart text-danger"></i>♡ Our Gallery ♡</h2>
          <div class="heart-grid">
            <div v-for="(item, index) in galleryItems" v-bind:key="index" v-bind:class="['heart-node', 'node-' + index]" v-on:click="openModal(item)">
              <div class="node-content">
                <video v-if="item.type === 'video'" muted loop onmouseover="this.play()" onmouseout="this.pause()">
                  <source v-bind:src="item.src" type="video/mp4">
                </video>
                <img v-else v-bind:src="item.src" class="heart-img" alt="Gallery memory">
              </div>
            </div>
          </div>
        </div>
        <Transition name="fade">
          <div v-if="showModal" class="custom-modal-overlay" v-on:click.self="closeModal">
            <div class="modal-wrapper">
              <button class="modal-close-btn" v-on:click="closeModal">&times;</button>
              <div class="modal-body">
                <img v-if="selectedItem.type === 'image'" v-bind:src="selectedItem.src" class="modal-media-resizer" alt="Selected memory">
                <video v-else controls autoplay class="modal-media-resizer">
                  <source v-bind:src="selectedItem.src" type="video/mp4">
                </video>
              </div>
            </div>
          </div>
        </Transition>
      </section>

      <section id="guestbook" class="mt-5 py-5 bg-light">
        <div class="container">
          <div class="guestbook-header text-center mb-5">
            <h2 class="arcade-font text-info">Guestbook</h2>
            <p class="text-dark small">Leave a message below! ✨</p>
          </div>
          <div class="row justify-content-center">
            <div class="col-md-7">
              <div class="guestbook-card-input mb-5">
                <input type="text" v-model="newGuestName" class="form-control mb-2" placeholder="Your Name...">
                <div class="input-wrapper d-flex">
                  <textarea v-model="newGuestMessage" class="form-control" placeholder="Your comment..."></textarea>
                  <button class="btn btn-primary ms-2" v-on:click="addComment">
                    <i class="fas fa-paper-plane"></i>
                  </button>
                </div>
              </div>
              <div class="comment-feed">
                <TransitionGroup name="list">
                  <div v-for="comment in guestbookComments" v-bind:key="comment.id" class="p-3 mb-3 border rounded border-secondary">
                    <div class="d-flex justify-content-between align-items-center">
                      <h6 class="text-info mb-0">{{ comment.name }}</h6>
                      <div class="d-flex align-items-center">
                        <small class="text-muted me-2">{{ comment.date }}</small>
                        <button v-on:click="deleteComment(comment.id)" class="btn btn-sm text-danger" title="Delete comment">
                          <i class="fas fa-trash"></i>
                        </button>
                      </div>
                    </div>
                    <hr class="my-2">
                    <p class="mt-2 mb-0 text-dark">{{ comment.message }}</p>
                  </div>
                </TransitionGroup>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section id="resources" class="py-5 bg-white">
        <div class="container">
          <div class="text-center mb-5">
            <h2 class="display-4 fw-bold">Resources & Credits</h2>
            <p class="lead text-muted">A special thanks to the tools and platforms that made this project possible.</p>
          </div>
          <div class="row g-4 justify-content-center">
            <div v-for="resource in resources" v-bind:key="resource.name" class="col-md-4 col-lg-3">
              <div class="card h-100 border-0 shadow-sm text-center p-3 resource-card">
                <div class="resource-icon mb-3">
                  <i v-bind:class="resource.icon + ' fa-3x text-primary'"></i>
                </div>
                <div class="card-body p-0">
                  <h5 class="card-title fw-bold">{{ resource.name }}</h5>
                  <p class="card-text small text-muted">{{ resource.description }}</p>
                  <a v-bind:href="resource.link" target="_blank" class="btn btn-outline-primary btn-sm stretched-link">
                    Visit Site
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>
</template>

<script setup>
  import { ref, reactive, onMounted } from 'vue';

let audioCtx;
let analyser;
let dataArray;
let source;

    const audioVisualData = ref(0);
    const activeProject = ref(null);
    const projects = ref([
      {
        id: "delivery",
        title: "(Project Rudy) Delivery App",
        subtitle: "Similar to Grab / Food Panda",
        desc: "A simple mobile delivery app featuring real-time tracking, order management, and a seamless checkout experience.",
        image: "./css/assets/delivery.png",
        media: [
          {
            type: "youtube",
            src: "https://www.youtube.com/embed/CfkjJd6pFHY",
            alt: "Delivery Ad Demo Video",
          },
          {
            type: "youtube",
            src: "https://www.youtube.com/embed/cY8D7BRjUfk",
            alt: "Delivery Ad 2 Video",
          },
        ],
      },
      {
        id: "game",
        title: "(Friendle) Interactive Choice Game",
        subtitle: "Chatting Strangers Parody",
        desc: "A web-based narrative experience mimicking random chat websites.",
        image: "./css/assets/chat.png",
      },
      {
        id: "ebook",
        title: "Voice Assisted E-Book",
        subtitle: "Accessibility-focused Reading",
        desc: "A simple python code with voice commands and text-to-speech technology.",
        image: "./css/assets/Ebook.png",
      },
      {
        id: "shoes",
        title: "(DropStock) Shoe Selling Website",
        subtitle: "Community Forum",
        desc: "Developed the social hub of the platform, allowing sneakerheads to discuss trends.",
        image: "./css/assets/shoe.png",
        media: [
          {
            type: "image",
            src: "./css/assets/dropstockdemo.png",
            alt: "DropStock Demo",
          },
          {
            type: "image",
            src: "./css/assets/dropstockdemo2.png",
            alt: "DropStock Demo 2",
          },
        ],
      },
      {
        id: "matchmake",
        title: "(La-Love) Love Tester",
        subtitle: "Front-end design",
        desc: "A matchmaking website where you measure your chance with your crush.",
        image: "./css/assets/love.png",
        media: [
          {
            type: "image",
            src: "./css/assets/matchmakedemo.png",
            alt: "Matchmake Demo",
          },
        ],
      },
    ]);

    const selectProject = (project) => {
      if (activeProject.value?.id === project.id) return;
      activeProject.value = project;
    };

    // --- HOBBIES & AUDIO LOGIC ---
    const activeHobby = ref("music");
    const selectedCD = ref(null);
    const audioPlayer = new Audio();

    const isPlaying = ref(false);
    const isMuted = ref(false);
    const audioProgress = ref(0);
    const audioVolume = ref(1);
    const rotationSpeed = ref("0s");

    const setupAnalyser = () => {
      if (!audioCtx) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        analyser = audioCtx.createAnalyser();
        source = audioCtx.createMediaElementSource(audioPlayer);
        source.connect(analyser);
        analyser.connect(audioCtx.destination);
        analyser.fftSize = 256;
        dataArray = new Uint8Array(analyser.frequencyBinCount);
      }
      if (audioCtx.state === "suspended") audioCtx.resume();
    };

    const hobbyData = ref({
      music: {
        title: "Music",
        icon: "fas fa-music",
        top5: [
          {
            name: "America's Next Freak",
            artist: "FM-Static",
            img: "./css/assets/song1.png",
            audio: "music1.mp3",
          },
          {
            name: "Teenage Dirtbag",
            artist: "Wheatus",
            img: "./css/assets/song2.png",
            audio: "music2.mp3",
          },
          {
            name: "Famous Last Words",
            artist: "My Chemical Romance",
            img: "./css/assets/song3.png",
            audio: "music3.mp3",
          },
          {
            name: "Tears Over Beers",
            artist: "Modern Baseball",
            img: "./css/assets/song4.png",
            audio: "music4.mp3",
          },
          {
            name: "Bullet proof Love",
            artist: "Pierce the Veil",
            img: "./css/assets/song5.png",
            audio: "music5.mp3",
          },
          {
            name: "Hard Times",
            artist: "Paramore",
            img: "./css/assets/song6.png",
            audio: "music6.mp3",
          },
        ],
      },
      games: {
        title: "Gaming",
        icon: "fas fa-ghost",
        selectedGame: null,
        items: [
          {
            name: "Valorant",
            device: "pc",
            color: "#ff4655",
            icon: "https://i.pinimg.com/1200x/f5/dd/24/f5dd24b3418701f617275cfa6a265ac8.jpg",
          },
          {
            name: "Roblox",
            device: "pc",
            color: "#4923c6ff",
            icon: "https://upload.wikimedia.org/wikipedia/commons/1/1e/Roblox_Logo_2025.png",
          },
          {
            name: "Minecraft",
            device: "pc",
            color: "#538b32",
            icon: "https://images.icon-icons.com/2699/PNG/512/minecraft_logo_icon_168974.png",
          },
          {
            name: "Mobile Legends",
            device: "mobile",
            color: "#d4ca3eff",
            icon: "https://downloadr2.apkmirror.com/wp-content/uploads/2024/01/45/65ba54423faa3_com.mobile.legends.png",
          },
          {
            name: "Discord: khaoss.x",
            device: "mobile",
            color: "#7753ecff",
            icon: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSZkjJsjxdWHZx1bu22YA_cJm7bicMd7d_pfw&s",
          },
        ],
      },
    });

    audioPlayer.ontimeupdate = () => {
      if (audioPlayer.duration)
        audioProgress.value =
          (audioPlayer.currentTime / audioPlayer.duration) * 100;
    };

    audioPlayer.onended = () => {
      isPlaying.value = false;
      audioProgress.value = 0;
      rotationSpeed.value = "0s";
    };

    const handleHobbyChange = (key) => {
      activeHobby.value = key;
      if (key !== "music") {
        audioPlayer.pause();
        isPlaying.value = false;
        selectedCD.value = null;
      }
    };

    const playCD = (cd) => {
      setupAnalyser();
      selectedCD.value = cd;
      audioPlayer.src = "./css/assets/" + cd.audio;
      audioPlayer.load();
      audioPlayer
        .play()
        .then(() => {
          isPlaying.value = true;
          rotationSpeed.value = "3s";
        })
        .catch((e) => console.error(e));
    };

    const togglePlay = () => {
      if (!selectedCD.value) return;
      setupAnalyser();
      if (audioPlayer.paused) {
        audioPlayer.play();
        isPlaying.value = true;
        rotationSpeed.value = "3s";
      } else {
        audioPlayer.pause();
        isPlaying.value = false;
        rotationSpeed.value = "0s";
      }
    };

    const updateVisuals = () => {
      if (analyser && isPlaying.value) {
        analyser.getByteFrequencyData(dataArray);
        let sum = 0;
        for (let i = 0; i < 12; i++) sum += dataArray[i];
        audioVisualData.value = sum / 12;

        const cdImg = document.querySelector(".cd-display img");
        if (cdImg) {
          const bass = audioVisualData.value;
          const hue = (Date.now() / 5) % 360;
          const intensity = bass / 25;
          const shakeX = (Math.random() - 0.5) * intensity;
          const shakeY = (Math.random() - 0.5) * intensity;
          const scale = 1 + bass / 150;

          cdImg.style.transform = `scale(${scale}) translate(${shakeX}px, ${shakeY}px)`;
          cdImg.style.filter = `
                        drop-shadow(0 0 ${
                          bass / 4
                        }px hsla(${hue}, 100%, 50%, 0.9))
                        drop-shadow(0 0 ${bass / 8}px white)
                        brightness(${1 + bass / 255})
                    `;
        }
      } else {
        audioVisualData.value = 0;
        const cdImg = document.querySelector(".cd-display img");
        if (cdImg) {
          cdImg.style.filter = "none";
          cdImg.style.transform = "scale(1)";
        }
      }
      requestAnimationFrame(updateVisuals);
    };
    updateVisuals();

    const restartAudio = () => {
      audioPlayer.currentTime = 0;
    };
    const toggleMute = () => {
      isMuted.value = !isMuted.value;
      audioPlayer.muted = isMuted.value;
    };
    const setVolume = (e) => {
      audioVolume.value = e.target.value;
      audioPlayer.volume = e.target.value;
    };
    const seekAudio = (e) => {
      if (!audioPlayer.duration) return;
      const rect = e.currentTarget.getBoundingClientRect();
      audioPlayer.currentTime =
        ((e.clientX - rect.left) / rect.width) * audioPlayer.duration;
    };

    const launchGame = (game) => {
      hobbyData.value.games.selectedGame = null;
      setTimeout(() => {
        hobbyData.value.games.selectedGame = game;
      }, 100);
    };

    // --- HEART GALLERY LOGIC ---
    const galleryItems = ref([
      { type: "image", src: "./css/assets/gallery/1.jpg" },
      { type: "image", src: "./css/assets/gallery/2.jpg" },
      { type: "image", src: "./css/assets/gallery/3.jpg" },
      { type: "image", src: "./css/assets/gallery/4.jpg" },
      { type: "image", src: "./css/assets/gallery/5.png" },
      { type: "image", src: "./css/assets/gallery/6.jpg" },
      { type: "image", src: "./css/assets/gallery/7.jpg" },
      { type: "image", src: "./css/assets/gallery/8.jpg" },
      { type: "video", src: "./css/assets/gallery/9.mp4" },
      { type: "image", src: "./css/assets/gallery/10.jpg" },
      { type: "image", src: "./css/assets/gallery/11.jpg" },
      { type: "image", src: "./css/assets/gallery/12.jpg" },
      { type: "image", src: "./css/assets/gallery/13.jpg" },
    ]);

    const showModal = ref(false);
    const selectedItem = ref(null);

    const openModal = (item) => {
      selectedItem.value = item;
      showModal.value = true;
      document.body.style.overflow = "hidden";
    };

    const closeModal = () => {
      showModal.value = false;
      selectedItem.value = null;
      document.body.style.overflow = "auto";
    };

    // --- GUESTBOOK LOGIC ---
    const guestbookComments = ref(
      JSON.parse(localStorage.getItem("portfolio-comments")) || []
    );
    const newGuestName = ref("");
    const newGuestMessage = ref("");
    const messageInput = ref(null);

    const focusMessage = () => {
      if (messageInput.value) messageInput.value.focus();
    };

    const addComment = () => {
      if (!newGuestName.value.trim() || !newGuestMessage.value.trim()) return;

      const newEntry = {
        id: Date.now(),
        name: newGuestName.value,
        message: newGuestMessage.value,
        date:
          new Date().toLocaleDateString() +
          " " +
          new Date().toLocaleTimeString([], {
            hour: "2-digit",
            minute: "2-digit",
          }),
      };

      guestbookComments.value.unshift(newEntry);
      localStorage.setItem(
        "portfolio-comments",
        JSON.stringify(guestbookComments.value)
      );

      // Reset
      newGuestName.value = "";
      newGuestMessage.value = "";
    };

    const deleteComment = (id) => {
      guestbookComments.value = guestbookComments.value.filter(
        (c) => c.id !== id
      );
      localStorage.setItem(
        "portfolio-comments",
        JSON.stringify(guestbookComments.value)
      );
    };

    const resources = ref([
      {
        name: "Google Search Engine",
        description: "Used to find images and programming tutorials.",
        icon: "fas fa-search",
        link: "https://google.com",
      },
      {
        name: "Font Awesome",
        description: "Scalable vector icons used throughout the interface.",
        icon: "fab fa-fort-awesome",
        link: "https://fontawesome.com",
      },
      {
        name: "Bootstrap",
        description: "Responsive framework for layout and components.",
        icon: "fab fa-bootstrap",
        link: "https://getbootstrap.com",
      },
      {
        name: "Canva",
        description: "UI Design and graphics creation.",
        icon: "fas fa-palette",
        link: "https://canva.com",
      },
      {
        name: "Gemini AI",
        description: "Help with logic, debugging, and code structure.",
        icon: "fas fa-microchip",
        link: "https://gemini.google.com/app",
      },
      {
        name: "Microsoft Co-pilot",
        description: "Assistance with complex logic and code generation.",
        icon: "fab fa-microsoft",
        link: "https://copilot.microsoft.com/",
      },
      {
        name: "Github",
        description: "Hosted code repository and webpage through Github Pages.",
        icon: "fas fa-github",
        link: "https://github.com/",
      },
      {
        name: "Emoji Combos",
        description: "For cute text and emoji decorations.",
        icon: "fas fa-heart",
        link: "https://emojicombos.com/heart",
      },
    ]);
    const activeEduImage = ref("./css/assets/apc.jpg");

    const changeEduImage = (newImage) => {
      activeEduImage.value = newImage;
    };

    onMounted(() => {
      initBopEffect();
      initVanillaLogic();
      initParticles();
      initLocalVideoPauser();

      window.addEventListener("keydown", (e) => {
        if (e.key === "Escape") closeModal();
      });
    });

// --- VANILLA FUNCTIONS ---

function initParticles() {
  const canvas = document.getElementById("particle-canvas");
  if (!canvas) return;

  canvas.style.position = "fixed";
  canvas.style.top = "0";
  canvas.style.left = "0";
  canvas.style.zIndex = "9999";
  canvas.style.pointerEvents = "none";

  const ctx = canvas.getContext("2d");
  let particles = [];
  const resize = () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  };
  window.addEventListener("resize", resize);
  resize();

  class Particle {
    constructor(x, y) {
      this.x = x;
      this.y = y;
      this.baseSize = Math.random() * 2 + 1.5;
      this.size = this.baseSize;
      this.speedX = (Math.random() - 0.5) * 4;
      this.speedY = (Math.random() - 0.5) * 4;
      this.life = 1.0;
      this.hue = (Date.now() / 10) % 360;
    }
    update(intensity) {
      this.x += this.speedX * (1 + intensity / 40);
      this.y += this.speedY * (1 + intensity / 40);
      this.size = this.baseSize + intensity / 15;
      this.life -= 0.012;
      this.hue = (this.hue + 2) % 360;
    }
    draw(intensity) {
      if (intensity > 1) {
        ctx.fillStyle = `hsla(${this.hue}, 100%, 65%, ${this.life})`;
        ctx.shadowBlur = intensity / 5;
        ctx.shadowColor = `hsla(${this.hue}, 100%, 50%, 0.8)`;
      } else {
        ctx.fillStyle = `rgba(200, 230, 255, ${this.life * 0.4})`;
        ctx.shadowBlur = 0;
      }
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fill();
      ctx.shadowBlur = 0;
    }
  }

  window.addEventListener("mousemove", (e) => {
    let count = audioVisualData.value > 30 ? 5 : 2;
    for (let i = 0; i < count; i++)
      particles.push(new Particle(e.clientX, e.clientY));
  });

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles = particles.filter((p) => p.life > 0);
    particles.forEach((p) => {
      p.update(audioVisualData.value);
      p.draw(audioVisualData.value);
    });
    requestAnimationFrame(animate);
  }
  animate();
}

function initLocalVideoPauser() {
  const expSection = document.getElementById("exp");
  if (!expSection) return;
  expSection.addEventListener("slide.bs.carousel", function () {
    const videos = expSection.querySelectorAll("video");
    videos.forEach((v) => v.pause());
    const iframes = expSection.querySelectorAll("iframe");
    iframes.forEach((i) => {
      const s = i.src;
      i.src = s;
    });
  });
}

function initVanillaLogic() {
  const shadow = document.querySelector(".cursor-shadow");
  window.addEventListener("mousemove", (e) => {
    const x = e.clientX + "px";
    const y = e.clientY + "px";
    document.documentElement.style.setProperty("--x", x);
    document.documentElement.style.setProperty("--y", y);
    if (shadow) {
      shadow.style.setProperty("--x", x);
      shadow.style.setProperty("--y", y);
    }
  });
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) entry.target.classList.add("reveal");
      });
    },
    { threshold: 0.05 }
  );
  document
    .querySelectorAll(".content-section")
    .forEach((s) => observer.observe(s));
}

function initBopEffect() {
  const targets = document.querySelectorAll(
    ".display-2, h2:not(.details-content h2), .bop-text"
  );
  targets.forEach((target) => {
    const text = target.textContent;
    if (!text) return;
    target.innerHTML = "";
    [...text].forEach((char) => {
      const span = document.createElement("span");
      span.textContent = char === " " ? "\u00A0" : char;
      span.classList.add("bop-letter");
      target.appendChild(span);
    });
  });
}


</script>

<style src="./css/style.css"></style>
