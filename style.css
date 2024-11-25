// Emoji Data with Real Event Structure Emojis
const emojiData = {
  Activities: ['🚗','🏃‍♂️','🧘‍♀️','🚴‍♀️','🏊‍♂️','🛹','🧗‍♂️','🏋️‍♀️','🤸‍♂️','🕺'],
  Cars: ['🚗','🚕','🚙','🚌','🚎','🏎️','🚓','🚑','🚒','🚐'],
  Wellness: ['🧘‍♀️','🏋️‍♀️','🛀','🧖‍♂️','🧗‍♀️','🤸‍♀️','🥋','🏄‍♂️','🤼‍♂️','🧘‍♂️'],
  // Additional categories as needed
};

// Current Category Index
let currentCategory = 'Activities';

// Function to load emojis into the grid
function loadEmojis() {
  const grid = document.getElementById('emoji-grid');
  grid.innerHTML = ''; // Clear existing emojis
  emojiData[currentCategory].forEach(emoji => {
    const emojiElement = document.createElement('div');
    emojiElement.classList.add('emoji-item');
    emojiElement.textContent = emoji;
    emojiElement.draggable = true;

    // Drag Events
    emojiElement.addEventListener('dragstart', dragStart);
    emojiElement.addEventListener('touchstart', touchStart, { passive: false });

    grid.appendChild(emojiElement);
  });
}

// Drag Functions
let draggedEmoji = null;

function dragStart(e) {
  draggedEmoji = e.target.textContent;
  e.dataTransfer.setData('text/plain', draggedEmoji);
}

// Drop Zone Events
const placeholders = document.querySelectorAll('.emoji-placeholder');

placeholders.forEach(placeholder => {
  placeholder.addEventListener('dragover', dragOver);
  placeholder.addEventListener('dragleave', dragLeave);
  placeholder.addEventListener('drop', drop);
});

function dragOver(e) {
  e.preventDefault();
  this.classList.add('highlight');
}

function dragLeave(e) {
  this.classList.remove('highlight');
}

function drop(e) {
  e.preventDefault();
  this.classList.remove('highlight');
  this.textContent = draggedEmoji;
  // Save state
  saveState();
}

// Touch Drag-and-Drop
function touchStart(e) {
  e.preventDefault();
  const touch = e.touches[0];
  draggedEmoji = e.target.textContent;

  const ghost = document.createElement('div');
  ghost.classList.add('emoji-item', 'ghost');
  ghost.style.position = 'absolute';
  ghost.style.left = `${touch.pageX - 15}px`;
  ghost.style.top = `${touch.pageY - 15}px`;
  ghost.textContent = draggedEmoji;
  document.body.appendChild(ghost);

  function moveTouch(e) {
    const touch = e.touches[0];
    ghost.style.left = `${touch.pageX - 15}px`;
    ghost.style.top = `${touch.pageY - 15}px`;

    // Highlight potential drop targets
    const elem = document.elementFromPoint(touch.clientX, touch.clientY);
    if (elem && elem.classList.contains('emoji-placeholder')) {
      elem.classList.add('highlight');
    } else {
      placeholders.forEach(ph => ph.classList.remove('highlight'));
    }
  }

  function endTouch(e) {
    const touch = e.changedTouches[0];
    const elem = document.elementFromPoint(touch.clientX, touch.clientY);
    if (elem && elem.classList.contains('emoji-placeholder')) {
      elem.textContent = draggedEmoji;
      elem.classList.remove('highlight');
      saveState();
    }
    ghost.remove();
    document.removeEventListener('touchmove', moveTouch);
    document.removeEventListener('touchend', endTouch);
    placeholders.forEach(ph => ph.classList.remove('highlight'));
  }

  document.addEventListener('touchmove', moveTouch, { passive: false });
  document.addEventListener('touchend', endTouch, { passive: false });
}

// Category Navigation
document.getElementById('next-category').addEventListener('click', () => {
  const categoryKeys = Object.keys(emojiData);
  let index = categoryKeys.indexOf(currentCategory);
  index = (index + 1) % categoryKeys.length;
  currentCategory = categoryKeys[index];
  document.getElementById('current-category').textContent = currentCategory;
  loadEmojis();
});

document.getElementById('prev-category').addEventListener('click', () => {
  const categoryKeys = Object.keys(emojiData);
  let index = categoryKeys.indexOf(currentCategory);
  index = (index - 1 + categoryKeys.length) % categoryKeys.length;
  currentCategory = categoryKeys[index];
  document.getElementById('current-category').textContent = currentCategory;
  loadEmojis();
});

// Reset Functionality
document.getElementById('reset-button').addEventListener('click', () => {
  placeholders.forEach(ph => ph.textContent = '');
  localStorage.removeItem('emojiState');
});

// Save and Load State
function saveState() {
  const state = {};
  placeholders.forEach((ph, index) => {
    state[index] = ph.textContent;
  });
  localStorage.setItem('emojiState', JSON.stringify(state));
}

function loadState() {
  const state = JSON.parse(localStorage.getItem('emojiState'));
  if (state) {
    placeholders.forEach((ph, index) => {
      if (state[index]) {
        ph.textContent = state[index];
      }
    });
  }
}

// Initialize
loadEmojis();
loadState();
