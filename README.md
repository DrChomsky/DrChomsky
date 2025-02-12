const fetch = require('node-fetch');
const fs = require('fs');

async function isUsernameAvailable(username) {
  const response = await fetch(`https://api.mojang.com/users/profiles/minecraft/${username}`);
  return response.status === 204; // Status 204 means the username is available
}

async function checkThreeLetterNames() {
  const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
  let availableNames = [];

  for (let i = 0; i < chars.length; i++) {
    for (let j = 0; j < chars.length; j++) {
      for (let k = 0; k < chars.length; k++) {
        let name = `${chars[i]}${chars[j]}${chars[k]}`;
        console.log(`Checking: ${name}`); // Display each name being checked
        let available = await isUsernameAvailable(name);
        if (available) {
          console.log(`✅ Available: ${name}`);
          availableNames.push(name);
        }
      }
    }
  }

  fs.writeFileSync('available-names.txt', availableNames.join('\n'));
  console.log(`✅ Found ${availableNames.length} available names. Saved to available-names.txt`);
}

checkThreeLetterNames();
