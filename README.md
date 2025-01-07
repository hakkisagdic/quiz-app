# quiz-app
Burak ile geliştirdiğimiz quiz app burada olacak.

**Quiz Uygulaması Geliştirme Rehberi**

### Projenin Amaç ve Hedefi
Bu projede amacın, React, Redux, Axios gibi modern frontend teknolojilerini kullanarak basit bir quiz uygulaması gelıştirmek ve pratik yapmaktır. Proje, sıfırdan geliştirilecek bir frontend yapısı içerirken, backend için hazır bir API kullanarak zaman kazanmanı sağlayacak.

---

### Kullanılacak Araçlar ve Teknolojiler
1. **React:** Dinamik ve bileşen tabanlı arayüzler oluşturmak için.
2. **Redux:** Uygulama durumunu (state) yönetmek için.
3. **Axios:** API'den veri çekmek için.
4. **HTML ve CSS:** Temel yapı ve stil için.
5. **Bootstrap:** Hazır şablonlar ve hızlı tasarım için.
6. **JSX:** HTML benzeri yapıları React bileşenlerinde yazmak için.
7. **JavaScript:** React bileşenlerinde işlevsellik sağlamak için.

---

### Adım Adım Geliştirme Rehberi

#### 1. **Projenin Hazırlık Aşaması**
- React uygulaması başlatmak için terminalde: `npx create-react-app quiz-app`
- İhtiyaç duyulan bağımlıkları yükle:
  ```bash
  npm install redux react-redux axios bootstrap react-bootstrap
  ```

#### 2. **Backend API'yi Seçme**

Projede hazır API kullanarak quiz verilerini çekeceksin. Örnek bir quiz API'si:
- **URL:** [Open Trivia Database API](https://opentdb.com/api_config.php)
- Endpoint: [https://opentdb.com/api.php?amount=10&type=multiple](https://opentdb.com/api.php?amount=10&type=multiple) (10 soruluk quiz)

#### 3. **Uygulama Yapısı**
Uygulama için aşağıdaki gibi bir dosya yapısı oluştur:

```
quiz-app/
├── src/
   ├── components/
   │   ├── Quiz.js
   │   ├── Question.js
   │   └── Result.js
   ├── redux/
   │   ├── actions.js
   │   └── reducer.js
   ├── App.js
   └── index.js
```

#### 4. **Redux Kurulumu**
- **State Yapısı:**
  ```javascript
  {
    questions: [],
    currentQuestionIndex: 0,
    score: 0,
    isFinished: false
  }
  ```
- `actions.js` dosyasına örnek bir action:
  ```javascript
  export const setQuestions = (questions) => ({
    type: 'SET_QUESTIONS',
    payload: questions,
  });
  ```
- `reducer.js` için örnek bir case:
  ```javascript
  const quizReducer = (state = initialState, action) => {
    switch (action.type) {
      case 'SET_QUESTIONS':
        return { ...state, questions: action.payload };
      default:
        return state;
    }
  };
  ```

#### 5. **API'den Veri Çekme**
- `Quiz.js` bileşeninde Axios kullanarak soruları çek:
  ```javascript
  import axios from 'axios';
  import { setQuestions } from '../redux/actions';
  import { useDispatch } from 'react-redux';

  const Quiz = () => {
    const dispatch = useDispatch();

    useEffect(() => {
      axios.get('https://opentdb.com/api.php?amount=10&type=multiple')
        .then(response => {
          const questions = response.data.results;
          dispatch(setQuestions(questions));
        });
    }, [dispatch]);

    return <div>Quiz App</div>;
  };
  ```

#### 6. **Bootstrap ile Arayüzü Geliştirme**
- Bootstrap komponentlerini kullanarak örnek bir tasarım:
  ```javascript
  import 'bootstrap/dist/css/bootstrap.min.css';

  const Question = ({ question }) => (
    <div className="card m-3">
      <div className="card-body">
        <h5 className="card-title">{question.question}</h5>
        {/* Şıkları buraya ekle */}
      </div>
    </div>
  );
  ```

#### 7. **Bitirme ve Sonraki Aşama**
- Projeyi tamamladıktan sonra:
  - Responsive tasarım testi yap.
  - Yeni özellikler düşün, örneğin zorluk seviyesini API'den alma.
  - Projeyi GitHub'a yükle ve paylaş.

---

### Ek Öneriler
- **React-Router kullan:** Quiz sonucu ve anasayfa arasında gezinmeyi sağla.
- **Form özellikleri ekle:** Kullanıcı adı girişi ve quiz başlatma.

Başarılar ve iyi çalışmalar!

