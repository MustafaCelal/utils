# Youtube Playlist duration
Youtube oynatma listelerinde videoların toplam süresini hesaplamak istiyorsan aşağıdaki kodu consola yapıştır.

```js
let totalHours = 0;
let totalMinutes = 0;
let totalSeconds = 0;

// get the playlist
const playlist = document.getElementsByClassName('style-scope ytd-playlist-video-list-renderer').contents.childNodes;

// iterate over each video
playlist.forEach(videoCard => {
    // extract the time information of the video and split it by the ":" character
    let timeInfo;
    
    if (videoCard.querySelector('#time-status')!=null && videoCard.querySelector('#time-status').innerText.includes(":")) {
      // İki nokta üst üste varsa normal bölme
      timeInfo = videoCard.querySelector('#time-status').innerText.trim().split(":");
    } else {
      return;
    }

    if (timeInfo.length === 2) {
        // if the duration has 2 elements (minutes and seconds)
        let minutes = parseInt(timeInfo[0]);
        let seconds = parseInt(timeInfo[1]);
        if (!isNaN(minutes) && !isNaN(seconds)) {
            totalMinutes += minutes;
            totalSeconds += seconds;
        }
    } else if (timeInfo.length === 3) {
        // if the duration has 3 elements (hours, minutes, and seconds)
        let hours = parseInt(timeInfo[0]);
        let minutes = parseInt(timeInfo[1]);
        let seconds = parseInt(timeInfo[2]);
        if (!isNaN(hours) && !isNaN(minutes) && !isNaN(seconds)) {
            totalHours += hours;
            totalMinutes += minutes;
            totalSeconds += seconds;
        }
    }
})

// convert minutes and seconds to hours
let totalMinutesResult = Math.floor(totalSeconds / 60) + totalMinutes;
let remainingSeconds = totalSeconds % 60;
let totalHoursResult = Math.floor(totalMinutesResult / 60) + totalHours;
let remainingMinutes = totalMinutesResult % 60;

// Print the calculated total duration
console.log("Total Time: " + totalHoursResult + " hours " + remainingMinutes + " minutes " + remainingSeconds + " seconds");
```
