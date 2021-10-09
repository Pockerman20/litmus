<img alt="LitmusChaos" src="https://avatars.githubusercontent.com/u/49853472?s=200&v=4" width="200" align="left">

# लिटमस
### ओपन सोर्स कैओस इंजीनियरिंग प्लेटफॉर्म

[![Slack Channel](https://img.shields.io/badge/Slack-Join-purple)](https://slack.litmuschaos.io)
![GitHub Workflow](https://github.com/litmuschaos/litmus/actions/workflows/push.yml/badge.svg?branch=master)
[![Docker Pulls](https://img.shields.io/docker/pulls/litmuschaos/chaos-operator.svg)](https://hub.docker.com/r/litmuschaos/chaos-operator)
[![GitHub stars](https://img.shields.io/github/stars/litmuschaos/litmus?style=social)](https://github.com/litmuschaos/litmus/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/litmuschaos/litmus)](https://github.com/litmuschaos/litmus/issues)
[![Twitter Follow](https://img.shields.io/twitter/follow/litmuschaos?style=social)](https://twitter.com/LitmusChaos)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/3202/badge)](https://bestpractices.coreinfrastructure.org/projects/3202)
[![BCH compliance](https://bettercodehub.com/edge/badge/litmuschaos/litmus?branch=master)](https://bettercodehub.com/)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Flitmuschaos%2Flitmus.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Flitmuschaos%2Flitmus?ref=badge_shield)
[![YouTube Channel](https://img.shields.io/badge/YouTube-Subscribe-red)](https://www.youtube.com/channel/UCa57PMqmz_j0wnteRa9nCaw)
<br><br><br><br>

#### *इसे [अन्य भाषाओं](translations/TRANSLATIONS.md) में पढ़ें।*

[🇰🇷](translations/README-ko.md) [🇨🇳](translations/README-chn.md) [🇯🇵](translations/README-ja.md)

## अवलोकन

लिटमस एक ओपन सोर्स कैओस इंजीनियरिंग प्लेटफॉर्म है जो टीमों को नियंत्रित तरीके से कैओस परीक्षणों को प्रेरित करके बुनियादी ढांचे में कमजोरियों और संभावित आउटेज की पहचान करने में सक्षम बनाता है।
डेवलपर्स और SREs आसानी से कैओस इंजीनियरिंग को लिटमस के साथ निष्पादित कर सकते हैं क्योंकि इसका उपयोग करना आसान है, आधुनिक कैओस इंजीनियरिंग प्रथाओं और समुदाय के सहयोग पर आधारित है।
लिटमस 100% खुला स्रोत और CNCF-होस्टेड है।

कैओस पैदा करने, प्रबंधित करने और निगरानी करने के लिए लिटमस क्लाउड-नेटिव दृष्टिकोण अपनाता है। प्लेटफ़ॉर्म स्वयं माइक्रोसर्विसेज के एक सेट के रूप में चलता है 
और कुबेरनेट्स कस्टम संसाधनों का उपयोग कैओस के इरादे, साथ ही स्थिर राज्य परिकल्पना को परिभाषित करने के लिए करता है।

उच्च स्तर पर, लिटमस में निम्न शामिल हैं:

- **Chaos Control Plane**: एक केंद्रीकृत कैओस प्रबंधन उपकरण जिसे कैओस-केंद्र कहा जाता है, जो लिटमस कैओस वर्कफ़्लोज़ के निर्माण, शेड्यूल और कल्पना में मदद करता है।

- **Chaos Execution Plane Services**: यह एक कैओस एजेंट और कई ऑपरेटरों से बना है जो एक परिभाषित लक्ष्य 
कुबेरनेट्स वातावरण के भीतर प्रयोग को निष्पादित और मॉनिटर करते हैं।

![वास्तुकला सारांश](/images/litmus-control-and-execution-plane-overview.png)

मंच के केंद्र में निम्नलिखित कैओस कस्टम संसाधन हैं:

- **ChaosExperiment**: यह किसी विशेष दोष के कॉन्फ़िगरेशन पैरामीटर को समूहित करने के लिए एक संसाधन हैं। कैओस एक्सपेरिमेंट CRs अनिवार्य रूप से इंस्टाल करने योग्य टेम्प्लेट हैं जो लाइब्रेरी में खराबी का वर्णन करते हैं, इसे चलाने के लिए आवश्यक अनुमतियों को इंगित करते हैं और इसके साथ काम करने वाले डिफ़ॉल्ट का वर्णन करते हैं।
कैओस एक्सपेरिमेंट के माध्यम से, लिटमस BYOC (ब्रिंग-योर-ओन-कैओस) का समर्थन करता है जो फॉल्ट इंजेक्शन करने के लिए किसी भी तृतीय-पक्ष टूलिंग को एकीकृत (वैकल्पिक) करने में मदद करता है।

- **ChaosEngine**: कुबेरनेट्स एप्लिकेशन वर्कलोड/सेवा, नोड या इंफ्रा घटक को कैओस एक्सपेरिमेंट द्वारा वर्णित दोष से जोड़ने के लिए एक संसाधन हैं।
यह चलने वाले गुणों को ट्यून करने और 'जांच' का उपयोग करके स्थिर स्थिति सत्यापन बाधाओं को निर्दिष्ट करने के विकल्प भी
प्रदान करता है। कैओस इंजिन को कैओस-ऑपरेटर द्वारा देखा जाता है, जो इसे धावकों के माध्यम से (प्रयोग निष्पादन को ट्रिगर करता है) समेट लेता है।

कैओस एक्सपेरिमेंट और कैओस इंजिन CRs एक वर्कफ़्लो ऑब्जेक्ट के भीतर अंतर्निहित किए गए हैं जो वांछित क्रम में एक या अधिक प्रयोगों को एक साथ बाँध कर रख सकते हैं।

- **ChaosResult**: यह प्रयोग चलाने के परिणामों को रखने के लिए एक संसाधन हैं। यह प्रत्येक सत्यापन बाधा की सफलता, गलती की वापसी/रोलबैक स्थिति के साथ-साथ फैसले का विवरण प्रदान करता है।
कैओस-निर्यातक परिणामों को पढ़ता है और प्रोमेथियस मेट्रिक्स के रूप में जानकारी को उजागर करता है।
कैओस परिणाम स्वचालित रन के दौरान विशेष रूप से उपयोगी होते हैं।

कैओस एक्सपेरिमेंट CRs को <a href="https://hub.litmuschaos.io" target="_blank">hub.litmuschaos.io</a> पर मेज़बान किया जाता है। यह एक केंद्रीय केंद्र है जहां
एप्लिकेशन डेवलपर्स या विक्रेता अपने कैओस प्रयोगों को साझा करते हैं ताकि उनके उपयोगकर्ता उत्पादन में अनुप्रयोगों के
लचीलेपन को बढ़ाने के लिए उनका उपयोग कर सकें। 

![कैओस-संचालक-प्रवाह](/images/chaos-operator-flow.png)

## उपयोग के मामले

- **डेवलपर्स के लिए**: इकाई परीक्षण या एकीकरण परीक्षण के विस्तार के रूप में आवेदन विकास के दौरान कैओस  प्रयोगों को चलाने के लिए।
- **सीआई/सीडी पाइपलाइन बिल्डरों के लिए**: पाइपलाइन चरण के रूप में कैओस  चलाने के लिए बग खोजने के लिए जब आवेदन पाइपलाइन में विफल पथों के अधीन होता है।
- **SREs के लिए**: आवेदन और/या आसपास के बुनियादी ढांचे में कैओस  प्रयोगों की योजना और अनुसूची के लिए ।
यह अभ्यास परिनियोजन प्रणाली में कमजोरियों की पहचान करता है और लचीलापन बढ़ाता है।

## लिटमस की व्याख्या

समझने के लिए <a href="https://docs.litmuschaos.io/docs/introduction/what-is-litmus" target="_blank">लिटमस डॉक्स</a> देखें।

## कैओस हब में योगदान

कैओस क्लब के लिए <a href="https://github.com/litmuschaos/community-charts/blob/master/CONTRIBUTING.md" target="_blank">योगदान दिशा निर्देशों की जांच </a> करें।


## समुदाय

सामुदायिक संसाधन:

यदि आपके कोई प्रश्न, चिंता या सुविधा अनुरोध हैं, तो बेझिझक संपर्क करें ।

- [ट्विटर](https://twitter.com/LitmusChaos) पर लिटमस कैओस को फॉलो करें ।

- नियमित अपडेट और मीटिंग रिकॉर्डिंग के लिए [लिटमस कैओस यूट्यूब चैनल](https://www.youtube.com/channel/UCa57PMqmz_j0wnteRa9nCaw) को सब्सक्राइब करें ।

- हमारे [स्लैक कम्युनिटी](https://slack.litmuschaos.io/) में शामिल होने और हमारे समुदाय के सदस्यों से मिलने के लिए, अपने प्रश्न और राय सामने रखें, [कुबेरनेट्स स्लैक](https://slack.k8s.io/) पर #litmus चैनल से जुड़ें।

### सामुदायिक बैठकें

लिटमस समुदाय की बैठक हर महीने के तीसरे बुधवार को 10:00PM IST/6:30 PM CEST/9.30 AM PST पर होती है ।

- [सिंक अप मीटिंग लिंक](https://zoom.us/j/91358162694)
- [सिंक अप एजेंडा और मीटिंग नोट्स](https://hackmd.io/a4Zu_sH4TZGeih-xCimi3Q)
- [रिलीज ट्रैकर](https://github.com/litmuschaos/litmus/milestones)

### वीडियो

- [लिटमस 2 - कैओस इंजीनियरिंग अर्गो वर्कफ़्लो से मिलती है](https://youtu.be/B8DfYnDh2F4) @ [DevOps टूलकिट](https://youtube.com/c/devopstoolkit)
- [लिटमस 2.0 के साथ हैंड्स-ऑन | Rawkode Live](https://youtu.be/D0t3emVLLko) @ [Rawkode Academy](https://www.youtube.com/channel/UCrber_mFvp_FEF7D9u8PDEA)
- [पेश है लिटमस कैओस 2.0 / Dok Talks #74](https://youtu.be/97BiCNtJbDw) @ [DoK.community](https://www.youtube.com/channel/UCUnXJbHQ89R2uSfKsqQwGvQ)
- [क्लाउड नेटिव कैओस इंजीनियरिंग का परिचय](https://youtu.be/LK0oDLQE4S8) @ [Kunal Kushwaha](https://www.youtube.com/channel/UCBGOUQHNNtNGcGzVq5rIXjw)
- [#EveryoneCanContribute कैफे: लिटमस - आपके कुबेरनेट्स के लिए कैओस इंजीनियरिंग](https://youtu.be/IiyrEiK4stQ) @ [GitLab Unfiltered](https://www.youtube.com/channel/UCMtZ0sc1HHNtGGWZFDRTh5A)
- [लिटमस - कुबेरनेट्स के लिए कैओस इंजीनियरिंग (CNCFMमिनट 9)](https://youtu.be/rDQ9XKbSJIc) @ [Saiyam Pathak](https://www.youtube.com/channel/UCi-1nnN0eC9nRleXdZA6ncg)
- [पृथ्वी राज द्वारा लिटमस कैओस के साथ कैओस इंजीनियरिंग || HACKODISHA Workshop](https://youtu.be/eyAG0svCsQA) @ [Webwiz](https://www.youtube.com/channel/UC9yM_PkV0QIIsPA3qPrp)

[और अधिक के लिए....](https://www.youtube.com/channel/UCa57PMqmz_j0wnteRa9nCaw)

### ब्लॉग

- CNCF: [लिटमस कैओस का परिचय](https://www.cncf.io/blog/2020/08/28/introduction-to-litmuschaos/)
- Hackernoon: [लिटमस कस्टम संसाधनों के माध्यम से कैओस का प्रबंधन और निगरानी](https://hackernoon.com/solid-tips-on-how-to-manage-and-monitor-chaos-via-litmus-custom-resources-5g1s33m9) 
- [कैओस में अवलोकनीयता संबंधी विचार: द मेट्रिक्स स्टोरी](https://dev.to/ksatchit/observability-considerations-in-chaos-the-metrics-story-6cb)

समुदाय ब्लॉग:

- Daniyal Rayn: [क्या मुझे अपने पर्यावरण पर कैओस इंजीनियरिंग की आवश्यकता है? मेरा विश्वास करो आपको इसकी आवश्यकता है!](https://maveric-systems.com/blog/do-i-need-chaos-engineering-on-my-environment-trust-me-you-need-it/)
- LiveWyer: [लिटमस कैओस शोकेस: हेल्म चार्ट टेस्ट सूट में कैओस प्रयोग](https://livewyer.io/blog/2021/03/22/litmuschaos-showcase-chaos-experiments-in-a-helm-chart-test-suite/)
- Jessica Cherry: [अपने टर्मिनल में कुबेरनेट क्लस्टर विफलताओं और प्रयोगों का परीक्षण](https://opensource.com/article/21/6/kubernetes-litmus-chaos)
- Yang Chuansheng(KubeSphere): [क्यूबस्फीयर 部署 लिटमस 至 कुबेरनेट्स 开启混沌实验](https://kubesphere.io/zh/blogs/litmus-kubesphere/)
- Saiyam Pathak(Civo): [आपका क्लस्टर उत्पादन के लिए तैयार है यह सुनिश्चित करने के लिए लिटमस का उपयोग करते हुए कुबेरनेट्स पर कैओस के प्रयोग](https://www.civo.com/learn/chaos-engineering-kubernetes-litmus)
- Andreas Krivas(Container Solutions):[कुबेरनेट्स वर्कलोड के लिए कैओस इंजीनियरिंग टूल्स की तुलना](https://blog.container-solutions.com/comparing-chaos-engineering-tools)
- Akram Riahi(WeScale):[कैओस इंजीनियरिंग: सभी कोणों से लिटमस](https://blog.wescale.fr/2021/03/11/chaos-engineering-litmus-sous-tous-les-angles/)
- Prashanto Priyanshu(LensKart):[कैओस इंजीनियरिंग के लिए लेंसकार्ट का दृष्टिकोण- भाग 2](https://blog.lenskart.com/lenskarts-approach-to-chaos-engineering-part-2-6290e4f3a74e)
- DevsDay.ru(Russian):[Kubecon EU '21 . में लिटमस कैओस](https://devsday.ru/blog/details/40746)
- Ryan Pei(Armory): [आपकी स्पिनाकर पाइपलाइन में लिटमस कैओस](https://www.armory.io/blog/litmuschaos-in-your-spinnaker-pipeline/)
- David Gildeh(Zebrium): [कुबेरनेट्स पर लिटमस कैओस इंजन के साथ स्वायत्त निगरानी का उपयोग करना](https://www.zebrium.com/blog/using-autonomous-monitoring-with-litmus-chaos-engine-on-kubernetes)

## एडॉप्टर्स

<a href="https://github.com/litmuschaos/litmus/blob/master/ADOPTERS.md" target="_blank">लिटमस कैओस के एडॉप्टर्</A>स की जांच करें

(यदि आप अपने कैओस  इंजीनियरिंग अभ्यास में लिटमस का उपयोग कर रहे हैं तो उपरोक्त पृष्ठ पर एक PR भेजें)

## लाइसेंस

लिटमस अपाचे लाइसेंस, संस्करण 2.0 के तहत लाइसेंस प्राप्त है। पूर्ण लाइसेंस पाठ के लिए [लाइसेंस](./LICENSE) देखें । लिटमस परियोजना द्वारा उपयोग की जाने वाली कुछ परियोजनाएं एक अलग लाइसेंस द्वारा नियंत्रित की जा सकती हैं, कृपया इसके विशिष्ट लाइसेंस का उल्लेख करें।

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Flitmuschaos%2Flitmus.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Flitmuschaos%2Flitmus?ref=badge_large)

लिटमस कैओस सीएनसीएफ परियोजनाओं का हिस्सा है।

[![CNCF](https://github.com/cncf/artwork/blob/master/other/cncf/horizontal/color/cncf-color.png)](https://landscape.cncf.io/selected=litmus)


## महत्वपूर्ण लिंक

<a href="https://docs.litmuschaos.io">
  लिटमस डॉक्स <img src="https://avatars0.githubusercontent.com/u/49853472?s=200&v=4" alt="Litmus Docs" height="15">
</a>
<br>
<a href="https://landscape.cncf.io/selected=litmus">
  सीएनसीएफ लैंडस्केप <img src="https://landscape.cncf.io/images/left-logo.svg" alt="Litmus on CNCF Landscape" height="15">
</a>
