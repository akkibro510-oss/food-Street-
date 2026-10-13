# FoodStreet — Fast Food Restaurant Listing Website

यह GitHub Pages + Firebase पर चलने वाला starter project है। इसमें पब्लिक लिस्टिंग, Google लॉगिन, रेस्टोरेंट आवेदन और प्राइवेट admin dashboard है।

## फ़ाइलें
- `index.html` — पब्लिक वेबसाइट और दुकान सबमिशन फॉर्म
- `admin.html` — एडमिन डैशबोर्ड
- `firestore.rules` — डेटा की सर्वर-साइड सुरक्षा नियम

## 1. Firebase प्रोजेक्ट बनाएँ
1. https://console.firebase.google.com/ खोलें और नया project बनाएँ।
2. Project settings → Your apps → Web app जोड़ें और Firebase config कॉपी करें।
3. `index.html` और `admin.html` में `firebaseConfig` की छह वैल्यू भरें।
4. Authentication → Sign-in method में **Google** सक्षम करें।
5. Authentication → Settings → Authorized domains में अपना GitHub Pages domain जोड़ें, जैसे `yourname.github.io`।
6. Firestore Database बनाएँ। Production mode चुनें।

## 2. अपने अकाउंट को Admin बनाएँ
1. `index.html` में Firebase config भरकर वेबसाइट को अस्थायी रूप से चलाएँ या localhost पर खोलें।
2. अपने Google अकाउंट से एक बार लॉगिन करें।
3. Firebase Console → Authentication → Users में अपना अकाउंट खोलें और उसका **UID** कॉपी करें।
4. उस UID को `admin.html` के `ADMIN_UID` में और `firestore.rules` में `PASTE_YOUR_GOOGLE_ACCOUNT_UID_HERE` की जगह डालें।
5. Firebase Console → Firestore Database → Rules में `firestore.rules` की सामग्री पेस्ट करके Publish करें।
6. UID किसी और को न दें। Admin UID बदलने पर HTML और Firestore Rules दोनों अपडेट करें।

> केवल admin.html में UID जाँचना सुरक्षा नहीं है। Firestore Rules ही असली सुरक्षा लागू करती हैं। नियम प्रकाशित किए बिना वेबसाइट को लाइव न करें।

## 3. GitHub पर लाइव करें
1. GitHub में नया repository बनाएँ, उदाहरण: `foodstreet`.
2. तीनों फ़ाइलें (`index.html`, `admin.html`, `firestore.rules`) repository में upload करें।
3. Repository → Settings → Pages → Deploy from a branch → `main` और `/ (root)` चुनें → Save।
4. कुछ मिनट बाद public URL खुलेगा: `https://YOUR_GITHUB_USERNAME.github.io/foodstreet/`
5. Admin URL: `https://YOUR_GITHUB_USERNAME.github.io/foodstreet/admin.html`

Admin URL सार्वजनिक रूप से खोजा जा सकता है, लेकिन गैर-अधिकृत Google अकाउंट को admin डेटा/कार्रवाई नहीं मिलेगी क्योंकि Firestore Rules उसे रोकती हैं।

## 4. दुकान verification workflow
- Owner Google से लॉगिन कर आवेदन भेजता है।
- आवेदन Firestore में `pending` स्टेटस के साथ सेव होता है।
- Admin `admin.html` में आवेदन जाँचता है और Approve या Reject करता है।
- Public homepage केवल `approved` स्टेटस वाले रेस्टोरेंट दिखाता है।

## 5. महत्वपूर्ण सीमाएँ और अगला चरण
- इस starter में वेरिफिकेशन डॉक्यूमेंट का प्रकार/विवरण लिया जाता है; **असली फाइल अपलोड और दस्तावेज़ सत्यापन अभी शामिल नहीं है**। संवेदनशील दस्तावेज़ को सार्वजनिक URL के रूप में न लें। Production में Firebase Storage, private storage rules और manual review जोड़ें।
- फोटो फ़ील्ड अभी image URL लेता है। सीधे फोटो अपलोड के लिए Firebase Storage जोड़ना होगा।
- मालिक के लिए अलग “मेरे आवेदन” डैशबोर्ड अभी शामिल नहीं है; वे फॉर्म सबमिट कर सकते हैं, लेकिन status देखने के लिए admin से संपर्क करना होगा।
- यह भोजन ऑर्डर/ऑनलाइन भुगतान प्रणाली नहीं है; यह restaurant directory है।
- Firestore Rules को publish करके test करें। Admin UID, Firebase config और Google sign-in domain ठीक सेट होने तक लॉगिन/डेटा काम नहीं करेगा।
- Public listing पर मालिक के मोबाइल नंबर दिखते हैं। अगर आप चाहें तो बाद में phone visibility toggle जोड़ें।
