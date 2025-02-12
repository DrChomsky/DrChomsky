const fs = require('fs');

const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
let names = [];

for (let i = 0; i < chars.length; i++) {
  for (let j = 0; j < chars.length; j++) {
    for (let k = 0; k < chars.length; k++) {
      names.push(`${chars[i]}${chars[j]}${chars[k]}`);
    }
  }
}

// Save to a file
fs.writeFileSync('three-letter-names.txt', names.join('\n'));
console.log(`✅ Generated ${names.length} names and saved to three-letter-names.txt`);
