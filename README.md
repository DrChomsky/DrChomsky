const fetch = require('node-fetch');

async function isUsernameAvailable(username) {
  const response = await fetch(`https://api.mojang.com/users/profiles/minecraft/${username}`);
  return response.status === 204;
}

(async () => {
  const chars = 'abcdefghijklmnopqrstuvwxyz0123456789_';
  for (let i = 0; i < chars.length; i++) {
    for (let j = 0; j < chars.length; j++) {
      for (let k = 0; k < chars.length; k++) {
        const username = `${chars[i]}${chars[j]}${chars[k]}`;
        if (await isUsernameAvailable(username)) {
          console.log(`${username} is available`);
        }
      }
    }
  }
})();

