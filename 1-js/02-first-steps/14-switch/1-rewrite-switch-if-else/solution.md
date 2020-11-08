`स्विच` की कार्यक्षमता का ठीक से मिलान करने के लिए, `इफ` को एक सख्त तुलना `===` का उपयोग करना चाहिए।

लेकिन `स्ट्रिंग` के लिए, एक सरल `==` भी काम करता है।

```js no-beautify
if(browser == 'Edge') {
  alert("You've got the Edge!");
} else if (browser == 'Chrome'
 || browser == 'Firefox'
 || browser == 'Safari'
 || browser == 'Opera') {
  alert( 'Okay we support these browsers too' );
} else {
  alert( 'We hope that this page looks ok!' );
}
```

कृपया ध्यान दें:  निर्माण `browser == 'Chrome' || browser == 'Firefox' …` बेहतर पठनीयता के लिए कई लाइनों में विभाजित है।

लेकिन `स्विच` निर्माण अभी भी स्वच्छ और अधिक वर्णनात्मक है।