<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Chronomètre Invisible</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      background: #f5f5f5;
    }
    h1 {
      margin-bottom: 30px;
    }
    button {
      padding: 12px 24px;
      margin: 6px;
      font-size: 1.1em;
      border: none;
      border-radius: 8px;
      background: #007bff;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background: #0056b3;
    }
    #laps {
      margin-top: 20px;
      max-width: 300px;
      width: 100%;
      background: white;
      padding: 12px;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    #laps p {
      margin: 6px 0;
      font-size: 0.95em;
      display: flex;
      justify-content: space-between;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <h1>Chronomètre Invisible</h1>
  <div>
    <button id="startStopBtn">Démarrer</button>
    <button id="toggleLapsBtn">Afficher les temps</button>
    <button id="resetBtn">Réinitialiser</button>
  </div>
  <div id="laps" class="hidden"></div>

  <script>
    let startTime = null;
    let isRunning = false;
    const lapsContainer = document.getElementById('laps');
    const startStopBtn = document.getElementById('startStopBtn');
    const toggleLapsBtn = document.getElementById('toggleLapsBtn');
    const resetBtn = document.getElementById('resetBtn');

    // Charger les temps depuis le localStorage
    let laps = JSON.parse(localStorage.getItem('laps')) || [];

    function saveLaps() {
      localStorage.setItem('laps', JSON.stringify(laps));
    }

    function renderLaps() {
      lapsContainer.innerHTML = '';
      if (laps.length === 0) {
        lapsContainer.innerHTML = '<p>Aucun temps enregistré.</p>';
        return;
      }
      laps.forEach(lap => {
        const p = document.createElement('p');
        const date = new Date(lap.timestamp);
        p.innerHTML = `<span>${date.toLocaleString()}</span><span>${formatDuration(lap.duration)}</span>`;
        lapsContainer.appendChild(p);
      });
    }

    function formatDuration(ms) {
      const totalSeconds = Math.floor(ms / 1000);
      const minutes = Math.floor(totalSeconds / 60);
      const seconds = totalSeconds % 60;
      const milliseconds = ms % 1000;
      return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}.${String(milliseconds).padStart(3, '0')}`;
    }

    startStopBtn.addEventListener('click', () => {
      if (!isRunning) {
        // Démarrage
        startTime = Date.now();
        isRunning = true;
        startStopBtn.textContent = 'Arrêter';
      } else {
        // Arrêt et enregistrement
        const endTime = Date.now();
        const duration = endTime - startTime;
        laps.unshift({ timestamp: endTime, duration });
        saveLaps();
        if (!lapsContainer.classList.contains('hidden')) renderLaps();
        isRunning = false;
        startStopBtn.textContent = 'Démarrer';
      }
    });

    toggleLapsBtn.addEventListener('click', () => {
      lapsContainer.classList.toggle('hidden');
      toggleLapsBtn.textContent = lapsContainer.classList.contains('hidden') ? 'Afficher les temps' : 'Cacher les temps';
      if (!lapsContainer.classList.contains('hidden')) renderLaps();
    });

    resetBtn.addEventListener('click', () => {
      if (confirm('Effacer tous les temps enregistrés ?')) {
        laps = [];
        saveLaps();
        renderLaps();
      }
    });
  </script>
</body>
</html>

<!--
  <<< Author notes: Course header >>>
  Include a 1280×640 image, course title in sentence case, and a concise description in emphasis.
  In your repository settings: enable template repository, add your 1280×640 social image, auto delete head branches.
  Add your open source license, GitHub uses MIT license.
-->

# GitHub Pages

_Create a site or blog from your GitHub repositories with GitHub Pages._

</header>

<!--
  <<< Author notes: Step 1 >>>
  Choose 3-5 steps for your course.
  The first step is always the hardest, so pick something easy!
  Link to docs.github.com for further explanations.
  Encourage users to open new tabs for steps!
-->

## Step 1: Enable GitHub Pages

_Welcome to GitHub Pages and Jekyll :tada:!_

The first step is to enable GitHub Pages on this [repository](https://docs.github.com/en/get-started/quickstart/github-glossary#repository). When you enable GitHub Pages on a repository, GitHub takes the content that's on the main branch and publishes a website based on its contents.

### :keyboard: Activity: Enable GitHub Pages

1. Open a new browser tab, and work on the steps in your second tab while you read the instructions in this tab.
1. Under your repository name, click **Settings**.
1. Click **Pages** in the **Code and automation** section.
1. Ensure "Deploy from a branch" is selected from the **Source** drop-down menu, and then select `main` from the **Branch** drop-down menu.
1. Click the **Save** button.
1. Wait about _one minute_ then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.
   > Turning on GitHub Pages creates a deployment of your repository. GitHub Actions may take up to a minute to respond while waiting for the deployment. Future steps will be about 20 seconds; this step is slower.
   > **Note**: In the **Pages** of **Settings**, the **Visit site** button will appear at the top. Click the button to see your GitHub Pages site.

<footer>

<!--
  <<< Author notes: Footer >>>
  Add a link to get support, GitHub status page, code of conduct, license link.
-->

---

Get help: [Post in our discussion board](https://github.com/orgs/skills/discussions/categories/github-pages) &bull; [Review the GitHub status page](https://www.githubstatus.com/)

&copy; 2023 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

</footer>
