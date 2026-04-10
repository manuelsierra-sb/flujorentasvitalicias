```mermaid
graph TD
    %% Inicio del Proceso
    Start([Entrada de Solicitud: Múltiples Canales]) --> A
    
    A[📧 Gmail <br> Buzón Centralizado: Correo de Rentas Vitalicias] --> B{⚙️ Google Apps Script <br> ¿Información Completa? <br> Ej. Cédula, Póliza}
    
    %% Validación de Datos
    B -- No --> C[📧 Gmail + ⚙️ Apps Script <br> Autorespuesta: Solicitar datos faltantes]
    C --> Espera([Espera de respuesta del usuario])
    
    %% Clasificación de Área
    B -- Sí --> D{⚙️ Google Apps Script <br> ¿Tema de Rentas Vitalicias?}
    D -- No --> E[⚙️ Google Apps Script <br> Redireccionar Síbol/Caso a Otra Área <br> Ej. ARL, Dir. Nac. Pensiones]
    E --> Fin1([Fin del flujo: Área Externa])
    
    %% Orquestador y Asignación
    D -- Sí --> F[⚙️ Google Apps Script <br> Analizar y Extraer Metadatos del Caso]
    F --> G{⚙️ Google Apps Script <br> Evaluación de Complejidad}
    
    G -- Fácil --> H[Lógica de Asignación: <br> Orden de llegada FIFO]
    G -- Difícil <br> Ej. Sustituciones, Derechos Petición --> I[Lógica de Asignación: <br> Distribución Equitativa Ponderada]
    
    H --> J{📊 Google Sheets / ⚙️ Apps Script <br> ¿Asesor Disponible? <br> Validar Ausencias}
    I --> J
    
    J -- No --> K[⚙️ Google Apps Script <br> Reasignar al siguiente Asesor Disponible]
    K --> L
    J -- Sí --> L[📧 Gmail + ⚙️ Apps Script <br> Asignar caso directamente al correo del Asesor]
    
    %% Notificaciones Paralelas
    L -.-> Notif[📧 Gmail + ⚙️ Apps Script <br> Sistema de Recordatorios: <br> Notificar casos próximos a vencer]
    
    %% Asistencia IA y Gestión Documental
    L --> M[✨ Gemini API / Vertex AI <br> IA Genera Sugerencia de Respuesta y unifica tono]
    M --> N[📁 Google Drive / 🗄️ Stelen <br> Actualizar Historial y <br> Crear carpetas por N° Póliza]
    
    %% Revisión y Salida
    N --> O[👩‍💻 Interfaz de Usuario / 📧 Gmail <br> Asesor Revisa, Ajusta y Envía Respuesta <br> desde buzón compartido]
    O --> P[⚙️ Google Apps Script <br> Orquestador analiza correos de salida <br> de la cuenta de Rentas Vitalicias]
    
    %% Cierre y Métricas
    P --> Q[⚙️ Google Apps Script <br> Marcar caso como Completado]
    Q --> R[📊 Google Sheets + Looker Studio <br> Calcular tiempo de cumplimiento y Métricas <br> Reemplazo de reportes Siol]
    R --> Fin2([Fin del flujo: Caso Cerrado])

    %% Estilos de Nodos
    classDef automatizado fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#000;
    classDef manual fill:#fff9c4,stroke:#fbc02d,stroke-width:2px,color:#000;
    classDef decision fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#000;
    classDef ia fill:#f3e5f5,stroke:#8e24aa,stroke-width:2px,color:#000;
    
    class A,B,C,D,F,G,H,I,J,K,L,N,P,Q,R,Notif automatizado;
    class E,O manual;
    class B,D,G,J decision;
    class M ia;
  
