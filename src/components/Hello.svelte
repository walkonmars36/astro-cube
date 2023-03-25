
<script>
 
 const words = [
  'Hi my name\'s Mark', 
  'I like CSS', 
  'I like JavaScript too', 
  'This is a new site I\'m building',
  'In Astro 🚀'
];

let part = words[0]; // Set the first string as the default static string
let i = 0;
let offset = 0;
const len = words.length;
let forwards = true;
let skip_count = 0;
const skip_delay = 15;
const speed = 70;

// Check if the user prefers reduced motion
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

// Show the first item if the user prefers reduced motion
if (prefersReducedMotion) {
  part = words[0];
 
}

function wordflick() {
  if (forwards) {
    if (offset >= words[i].length) {
      ++skip_count;
      if (skip_count == skip_delay) {
        forwards = false;
        skip_count = 0;
      }
    }
  }
  else {
    if (offset == 0) {
      forwards = true;
      i++;
      offset = 0;
      if (i >= len) {
        i = 0;
      }
    }
  }
  part = words[i].substring(0, offset);
  if (skip_count == 0) {
    if (forwards) {
      offset++;
    }
    else {
      offset--;
    }
  }
}
    setInterval(() => {
      wordflick();
    }, speed);

</script>
  
<h1>{part}</h1>

