# रात का चिराग़ बनाएं - रास्पबेरी पाई

पाठ के इस भाग में, आप अपने रास्पबेरी पाई में एक एलईडी जोड़ेंगे और इसका उपयोग रात का चिराग़ बनाने के लिए करेंगे।

## हार्डवेयर

नाइटलाइट को अब एक एक्चुएटर की जरूरत है।

एक्चुएटर एक **LED**, एक [प्रकाश उत्सर्जक डायोड](https://wikipedia.org/wiki/Light-emmitting_diode) है जो करंट प्रवाहित होने पर प्रकाश का उत्सर्जन करता है। यह एक डिजिटल एक्ट्यूएटर है जिसमें 2 स्थिति हैं, चालू और बंद। 1 का मान भेजने से एलईडी चालू हो जाती है, और 0 इसे बंद कर देता है। एलईडी एक बाहरी ग्रोव एक्ट्यूएटर है और इसे रास्पबेरी पाई पर ग्रोव बेस हैट से जोड़ा जाना चाहिए।

सुडो कोड में नाइटलाइट तर्क है:

```आउटपुट
प्रकाश स्तर की जाँच करें।
यदि प्रकाश 300 . से कम है
    एलईडी चालू करें
अन्यथा
    एलईडी बंद करें
```

### एलईडी कनेक्ट करें

ग्रोव एलईडी एलईडी के चयन के साथ एक मॉड्यूल के रूप में आता है, जिससे आप रंग चुन सकते हैं।

#### कार्य - एलईडी कनेक्ट करें

एलईडी कनेक्ट करें।

![एक ग्रोव एलईडी](../../../images/grove-led.png)

1. अपनी पसंदीदा एलईडी चुनें और इसके पैरों को एलईडी मॉड्यूल के दो छेदों में डालें।

    एल ई डी प्रकाश उत्सर्जक डायोड हैं, और डायोड इलेक्ट्रॉनिक उपकरण हैं जो केवल एक ही तरह से करंट ले जा सकते हैं। इसका मतलब है कि एलईडी को सही तरीके से जोड़ने की जरूरत है, अन्यथा यह काम नहीं करेगा।

    एलईडी के पैरों में से एक पॉसिटिव पिन है, दूसरा नेगेटिव पिन है। एलईडी पूरी तरह गोल नहीं है और एक तरफ से थोड़ी चपटी है। थोड़ा बढ़ा हुआ पक्ष नेगेटिव पिन है। जब आप एलईडी को मॉड्यूल से कनेक्ट करते हैं, तो सुनिश्चित करें कि गोलाकार तरफ वाला पिन मॉड्यूल के बाहर + चिह्नित सॉकेट से जुड़ा है, और बढ़ा हुआा पक्ष सॉकेट से मध्य के करीब जुड़ा हुआ है।

1. एलईडी मॉड्यूल में एक स्पिन बटन है जो आपको चमक को नियंत्रित करने की अनुमति देता है। इसे शुरू करने के लिए इसे दक्षिणावर्त घुमाकर शुरू करें, जहां तक ​​​​यह एक छोटे से फिलिप्स हेड स्क्रूड्राइवर का उपयोग करके जाएगा।

1. एलईडी मॉड्यूल पर सॉकेट में ग्रोव केबल का एक सिरा डालें। यह केवल एक ही तरह से घूमेगा।

1. रास्पबेरी पाई के बंद होने के साथ, ग्रोव केबल के दूसरे छोर को पाई से जुड़ी ग्रोव बेस हैट पर **D5** चिह्नित डिजिटल सॉकेट से कनेक्ट करें। यह सॉकेट GPIO पिन के बगल में सॉकेट की पंक्ति में बाईं ओर से दूसरा है।

![सॉकेट D5 से जुड़ी ग्रोव एलईडी](../../../images/pi-led.png)

## रात के उजाले का प्रोग्राम

नाइटलाइट को अब ग्रोव लाइट सेंसर और ग्रोव एलईडी का उपयोग करके प्रोग्राम किया जा सकता है।

### कार्य - रात के चिराग़ का प्रोग्राम

रात के समय प्रोग्राम करें।

1. पाई को पावर दें और इसके बूट होने की प्रतीक्षा करें

1. वीएस कोड में नाइटलाइट प्रोजेक्ट खोलें जिसे आपने इस असाइनमेंट के पिछले भाग में बनाया था, या तो सीधे पाई पर चल रहा है या रिमोट एसएसएच एक्सटेंशन का उपयोग करके जुड़ा हुआ है।

1. आवश्यक लाइब्रेरी आयात करने के लिए कनेक्ट करने के लिए `app.py` फ़ाइल में निम्न कोड जोड़ें। इसे अन्य `import` लाइनों के नीचे, शीर्ष पर जोड़ा जाना चाहिए।

    ```python
    from grove.grove_led import GroveLed
    ```

    `from Grove.grove_led import GroveLed` कथन GroveLed` को Grove Python पुस्तकालयों से आयात करता है। इस पुस्तकालय में ग्रोव एलईडी के साथ बातचीत करने के लिए कोड है।

1. एलईडी का प्रबंधन करने वाले वर्ग का एक उदाहरण बनाने के लिए `light_sensor` घोषणा के बाद निम्नलिखित कोड जोड़ें:

    ```python
    led = GroveLed(5)
    ```

    लाइन `led = GroveLed(5)` `GroveLed` वर्ग को पिन से जोड़ने का एक उदाहरण बनाता है **D5** - वह डिजिटल ग्रोव पिन जिससे एलईडी जुड़ा है।

    > 💁 सभी सॉकेट में अद्वितीय पिन नंबर होते हैं। पिन 0, 2, 4, और 6 एनालॉग पिन हैं, पिन 5, 16, 18, 22, 24 और 26 डिजिटल पिन हैं।

1. प्रकाश के स्तर की जांच करने और एलईडी को चालू या बंद करने के लिए `while` लूप के अंदर, और `time.sleep` से पहले एक चेक जोड़ें:

    ```python
    if light < 300:
        led.on()
    else:
        led.off()
    ```

    यह कोड `light` के मूल्य की जांच करता है। यदि यह ३०० से कम है तो यह `GroveLed` वर्ग की `on` विधि को कॉल करता है जो एलईडी को 1 का डिजिटल मान भेजता है, इसे चालू करता है। यदि प्रकाश मान ३०० से अधिक या उसके बराबर है, तो यह `off` विधि को कॉल करता है, एलईडी को 0 का डिजिटल मान भेजकर, इसे बंद कर देता है।

    > 💁 इस कोड को `print('Light level:', light)` लाइन के समान स्तर पर इंडेंट किया जाना चाहिए, while loop के अंदर होना चाहिए!

    > 💁 एक्ट्यूएटर्स को डिजिटल मान भेजते समय, 0 मान 0V होता है, और 1 मान डिवाइस के लिए अधिकतम वोल्टेज होता है। ग्रोव सेंसर और एक्चुएटर्स के साथ रास्पबेरी पाई के लिए, 1 वोल्टेज 3.3V है।

1. वीएस कोड टर्मिनल से, अपना पायथन ऐप चलाने के लिए निम्नलिखित चलाएँ:

   ```sh
    python3 app.py
    ```

    कंसोल के लिए लाइट मान आउटपुट होंगे।

    ```output
    pi@raspberrypi:~/nightlight $ python3 app.py 
    Light level: 634
    Light level: 634
    Light level: 634
    Light level: 230
    Light level: 104
    Light level: 290
    ```

1. प्रकाश संवेदक को ढकें और उजागर करें। ध्यान दें कि यदि प्रकाश का स्तर 300 या उससे कम है, तो एलईडी कैसे जलेगी, और जब प्रकाश का स्तर 300 से अधिक हो तो बंद कर दें।

    > 💁 यदि एलईडी चालू नहीं होती है, तो सुनिश्चित करें कि यह सही तरीके से जुड़ा हुआ है, और स्पिन बटन को सेट किया गया है
    
![प्रकाश स्तर में परिवर्तन के रूप में पाई से जुड़ी एलईडी चालू और बंद हो जाती है](../../../images/pi-running-assignment-1-1.gif)

> 💁 आप इस कोड को [code-actuator/pi](code-actuator/pi) फोल्डर में पा सकते हैं।

😀आपका रात्रिकालीन प्रोग्राम सफल रहा!