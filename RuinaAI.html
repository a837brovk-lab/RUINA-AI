import React, { useState, useEffect } from 'react';
import { ShieldCheck, ShieldAlert, Check, Image as ImageIcon, Loader2, Sparkles, Download, Aperture, Lock, Upload, X } from 'lucide-react';

const API_KEY = ""; // Ключ будет подставлен автоматически
const IMAGE_EDITING_MODEL = "gemini-2.5-flash-image-preview";

export default function App() {
  const [step, setStep] = useState('auth');
  const [prompt, setPrompt] = useState('');
  const [generatedImage, setGeneratedImage] = useState(null);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);
  const [uploadedImageBase64, setUploadedImageBase64] = useState(null);
  const [uploadedImageMimeType, setUploadedImageMimeType] = useState(null);

  // --- Image Upload Handler ---
  const handleImageUpload = (event) => {
    const file = event.target.files[0];
    if (!file) return;

    if (!file.type.startsWith('image/')) {
        setError('Пожалуйста, загрузите файл изображения (jpeg, png).');
        setUploadedImageBase64(null);
        setUploadedImageMimeType(null);
        return;
    }
    
    setError(null);
    setUploadedImageMimeType(file.type);

    const reader = new FileReader();
    reader.onload = (e) => {
      // Base64 string includes the header "data:image/jpeg;base64,", we need to remove it
      const base64Data = e.target.result.split(',')[1];
      setUploadedImageBase64(base64Data);
    };
    reader.readAsDataURL(file);
  };

  const removeImage = () => {
    setUploadedImageBase64(null);
    setUploadedImageMimeType(null);
    // Сбросить генерацию, если она была с этим фото
    if (generatedImage) setGeneratedImage(null); 
    setError(null);
  };

  // --- Generation Logic ---
  const performGeneration = async (currentPrompt, base64Image, mimeType) => {
    // Проверка, что есть либо текст, либо изображение
    if (!currentPrompt && !base64Image) return;

    setIsLoading(true);
    setError(null);
    setGeneratedImage(null);

    try {
      // 1. Формируем список частей (parts) для API
      const parts = [];
      if (currentPrompt) {
          parts.push({ text: currentPrompt });
      } else if (!base64Image) {
          // Если нет текста, но нет и изображения, выходим
          throw new Error('Введите описание или загрузите изображение для редактирования.');
      }
      
      // Добавляем изображение, если оно есть
      if (base64Image && mimeType) {
        parts.push({
          inlineData: {
            mimeType: mimeType,
            data: base64Image
          }
        });
      }

      // 2. Создаем Payload
      const payload = {
          contents: [{ role: "user", parts: parts }],
          generationConfig: {
              responseModalities: ['IMAGE']
          },
      };

      // 3. Вызываем API
      const response = await fetch(
        `https://generativelanguage.googleapis.com/v1beta/models/${IMAGE_EDITING_MODEL}:generateContent?key=${API_KEY}`,
        {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(payload),
        }
      );

      if (!response.ok) throw new Error('Не удалось сгенерировать изображение. Возможно, описание слишком сложное.');

      const data = await response.json();
      
      // 4. Обрабатываем ответ
      const base64Data = data?.candidates?.[0]?.content?.parts?.find(p => p.inlineData)?.inlineData?.data;

      if (base64Data) {
        setGeneratedImage(`data:image/png;base64,${base64Data}`);
      } else {
        throw new Error('Сервер не вернул данные изображения. Попробуйте другой запрос.');
      }

    } catch (err) {
      setError(err.message || 'Произошла ошибка при генерации');
      setGeneratedImage(null);
    } finally {
      setIsLoading(false);
    }
  };
  
  // Эффект с отложенным запуском (Debounce Effect)
  useEffect(() => {
    // Условие: генерировать, если есть хотя бы 1 символ ИЛИ есть загруженное изображение.
    const shouldGenerate = prompt.trim().length >= 1 || uploadedImageBase64;
    
    if (!shouldGenerate) {
        setGeneratedImage(null);
        setIsLoading(false);
        return;
    }

    setIsLoading(true);
    
    const handler = setTimeout(() => {
        performGeneration(prompt, uploadedImageBase64, uploadedImageMimeType);
    }, 1000); // Задержка 1000 мс (1 секунда)

    return () => {
        clearTimeout(handler);
    };
  }, [prompt, uploadedImageBase64, uploadedImageMimeType]); // Зависимость: эффект срабатывает при изменении 'prompt' или изображения

  // Ручной запуск (для кнопки и Enter)
  const handleManualGeneration = () => {
      // Проверка: нужен хотя бы 1 символ ИЛИ загруженное изображение.
      if (prompt.trim().length >= 1 || uploadedImageBase64) {
          setError(null); // Сброс ошибки, если условия выполнены
          performGeneration(prompt, uploadedImageBase64, uploadedImageMimeType);
      } else {
          setError('Введите описание (минимум 1 символ) ИЛИ загрузите фото для редактирования.');
          setGeneratedImage(null);
      }
  };


  const handleDownload = () => {
    if (generatedImage) {
      const link = document.createElement('a');
      link.href = generatedImage;
      link.download = `ruina-gen-${Date.now()}.png`;
      link.click();
    }
  };

  // --- UI Components for Auth and Denied screens (unchanged) ---

  // Экран проверки безопасности (Clean Professional Dark)
  if (step === 'auth') {
    return (
      <div className="min-h-screen bg-slate-950 flex items-center justify-center p-4 font-sans text-slate-100">
        <div className="bg-slate-900 rounded-2xl border border-slate-800 shadow-2xl max-w-md w-full p-8 text-center">
          
          <div className="mb-6 flex justify-center">
            <div className="bg-blue-500/10 p-4 rounded-full border border-blue-500/20">
              <ShieldCheck size={48} className="text-blue-500" />
            </div>
          </div>

          <h2 className="text-2xl font-bold text-white mb-2">
            Проверка доступа
          </h2>
          <p className="text-slate-400 mb-8 text-sm">
            Для использования сервиса Ruina AI необходимо подтвердить личность.
          </p>

          <div className="bg-slate-800/50 rounded-xl p-4 mb-8 border border-slate-700">
            <p className="text-lg font-medium text-slate-200">
              Ваша фамилия <span className="text-blue-400 font-bold">Сергеенка</span>?
            </p>
          </div>

          <div className="grid grid-cols-2 gap-4">
            <button
              onClick={() => setStep('denied')}
              className="bg-slate-800 hover:bg-slate-700 text-slate-300 font-medium py-3 px-6 rounded-xl transition-all border border-slate-700 hover:border-slate-600"
            >
              Да, это я
            </button>
            <button
              onClick={() => setStep('app')}
              className="bg-blue-600 hover:bg-blue-500 text-white font-bold py-3 px-6 rounded-xl transition-all shadow-lg shadow-blue-900/20"
            >
              Нет
            </button>
          </div>
          
          <p className="mt-6 text-xs text-slate-600">Secure Access v1.0</p>
        </div>
      </div>
    );
  }

  // Экран отказа (Clean Professional Dark)
  if (step === 'denied') {
    return (
      <div className="min-h-screen bg-slate-950 flex items-center justify-center p-4 font-sans">
        <div className="bg-slate-900 rounded-2xl border border-red-900/30 p-8 text-center max-w-md w-full shadow-2xl">
          <div className="flex justify-center mb-6">
            <div className="bg-red-500/10 p-4 rounded-full">
              <Lock size={64} className="text-red-500" />
            </div>
          </div>
          <h1 className="text-2xl font-bold text-white mb-4">
            Доступ ограничен
          </h1>
          <p className="text-slate-400 mb-8">
            К сожалению, политика использования сервиса ограничивает доступ для пользователей с фамилией Сергеенка.
          </p>
          <button
            onClick={() => setStep('auth')}
            className="text-blue-500 hover:text-blue-400 text-sm font-medium hover:underline"
          >
            Вернуться назад
          </button>
        </div>
      </div>
    );
  }

  // --- Main App UI ---
  return (
    <div className="min-h-screen bg-slate-950 flex flex-col font-sans text-slate-100">
      {/* Header */}
      <header className="bg-slate-900/50 backdrop-blur-md border-b border-slate-800 sticky top-0 z-20">
        <div className="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="bg-blue-600 p-2 rounded-lg shadow-lg shadow-blue-900/20">
              <Aperture size={24} className="text-white" />
            </div>
            <span className="text-xl font-bold tracking-tight text-white">
              Ruina <span className="text-blue-500 font-light">AI</span>
            </span>
          </div>
          <div className="flex items-center gap-2">
            <div className="h-2 w-2 rounded-full bg-green-500 animate-pulse"></div>
            <span className="text-xs font-medium text-slate-400">Online</span>
          </div>
        </div>
      </header>

      {/* Main Content */}
      <main className="flex-1 max-w-6xl w-full mx-auto p-4 md:p-8 flex flex-col gap-6">
        
        {/* Input Area */}
        <div className="bg-slate-900 rounded-2xl p-4 shadow-lg border border-slate-800">
            <div className="flex flex-col md:flex-row gap-2 bg-slate-950/50 rounded-xl p-2">
                
                {/* Text Input */}
                <input
                    type="text"
                    value={prompt}
                    onChange={(e) => {
                        setPrompt(e.target.value);
                        setError(null); // Сброс ошибки при начале печати
                    }}
                    placeholder={uploadedImageBase64 ? 
                        "Введите команду для редактирования (например: убери брови)" : 
                        "Введите описание для генерации (минимум 1 символ)..."
                    }
                    className="flex-1 bg-transparent text-white px-4 py-3 focus:outline-none placeholder:text-slate-600 font-medium"
                    onKeyDown={(e) => e.key === 'Enter' && handleManualGeneration()}
                />

                {/* Upload Button */}
                <label className="flex items-center justify-center bg-slate-800 hover:bg-slate-700 text-white font-semibold py-3 px-4 rounded-lg transition-all cursor-pointer min-w-[120px]">
                    <Upload size={18} className="mr-2" />
                    {uploadedImageBase64 ? 'Заменить' : 'Загрузить Фото'}
                    <input 
                        type="file" 
                        accept="image/jpeg, image/png" 
                        onChange={handleImageUpload} 
                        className="hidden" 
                    />
                </label>

                {/* Create Button */}
                <button
                    onClick={handleManualGeneration}
                    disabled={isLoading || (!prompt.trim() && !uploadedImageBase64)}
                    className="bg-blue-600 hover:bg-blue-500 disabled:bg-slate-800 disabled:text-slate-600 text-white font-semibold py-3 px-6 rounded-lg transition-all flex items-center justify-center gap-2 min-w-[160px] shadow-lg shadow-blue-900/20"
                >
                    {isLoading ? (
                        <>
                            <Loader2 className="animate-spin" size={18} />
                            Генерация...
                        </>
                    ) : (
                        <>
                            <Sparkles size={18} />
                            Создать
                        </>
                    )}
                </button>
          </div>
          {error && (
            <div className="px-2 pb-2 pt-3">
                <div className="text-red-400 text-sm flex items-center gap-2 bg-red-950/20 border border-red-900/30 p-3 rounded-lg">
                <ShieldAlert size={16} />
                {error}
                </div>
            </div>
          )}

          {/* Uploaded Image Preview */}
          {uploadedImageBase64 && (
            <div className="mt-4 p-3 bg-slate-800 rounded-lg flex items-center justify-between border border-slate-700">
                <div className="flex items-center gap-3">
                    <img 
                        src={`data:${uploadedImageMimeType};base64,${uploadedImageBase64}`} 
                        alt="Uploaded" 
                        className="w-10 h-10 object-cover rounded-md border border-slate-600"
                    />
                    <span className="text-sm text-slate-300">
                        {uploadedImageMimeType.split('/')[1].toUpperCase()} файл загружен. 
                        <span className="text-blue-400 ml-2">Режим: Редактирование.</span>
                    </span>
                </div>
                <button onClick={removeImage} className="text-slate-500 hover:text-white transition-colors p-1 rounded-full">
                    <X size={18} />
                </button>
            </div>
          )}
        </div>

        {/* Result Area */}
        <div className="flex-1 bg-slate-900 rounded-2xl border border-slate-800 min-h-[500px] flex flex-col relative overflow-hidden shadow-2xl">
          
          {/* Subtle Background Pattern */}
          <div className="absolute inset-0 opacity-30" style={{ backgroundImage: 'radial-gradient(#1e293b 1px, transparent 1px)', backgroundSize: '24px 24px' }}></div>

          <div className="flex-1 flex items-center justify-center p-8 relative z-10">
            {generatedImage ? (
              <div className="relative group max-w-full">
                <img 
                  src={generatedImage} 
                  alt="Generated Result" 
                  className="max-w-full max-h-[600px] rounded-lg shadow-2xl border border-slate-700"
                />
              </div>
            ) : (
              <div className="text-center text-slate-700 select-none">
                {isLoading ? (
                  <div className="flex flex-col items-center gap-6">
                    <Loader2 size={48} className="text-blue-500 animate-spin" />
                    <p className="text-blue-400/80 text-sm font-medium animate-pulse">
                      Нейросеть создает изображение...
                    </p>
                  </div>
                ) : (
                  <div className="flex flex-col items-center gap-4 opacity-60">
                    <div className="bg-slate-800 p-6 rounded-full border border-slate-700">
                        <ImageIcon size={48} className="text-slate-500" />
                    </div>
                    <p className="text-slate-500 font-medium">Здесь появится результат</p>
                  </div>
                )}
              </div>
            )}
          </div>

          {/* Action Bar */}
          {(generatedImage || (uploadedImageBase64 && !isLoading)) && (
            <div className="border-t border-slate-800 bg-slate-900/90 p-4 flex justify-between items-center backdrop-blur-sm relative z-20 rounded-b-2xl">
              <div className="text-xs text-slate-500 font-mono">
                {generatedImage ? `ID: ${Date.now().toString().slice(-8)}` : 'Ожидание генерации...'}
              </div>
              {generatedImage && (
                <button
                  onClick={handleDownload}
                  className="bg-white hover:bg-slate-200 text-slate-900 font-semibold py-2 px-4 rounded-lg flex items-center gap-2 transition-all shadow-lg"
                >
                  <Download size={18} />
                  Скачать PNG
                </button>
              )}
            </div>
          )}
        </div>
      </main>

      {/* Footer */}
      <footer className="p-6 text-center mt-auto border-t border-slate-900">
        <p className="text-slate-600 text-sm">
          © 2025 Ruina AI Systems. All rights reserved.
        </p>
      </footer>
    </div>
  );
}
