<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agujero Negro Interstellar</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            width: 100%;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #0a0e27 0%, #16213e 50%, #0f3460 100%);
            font-family: 'Arial', sans-serif;
            overflow: hidden;
        }
        
        .container {
            position: relative;
            width: 600px;
            height: 600px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        /* Círculo de acreción exterior */
        .accretion-disk {
            position: absolute;
            border-radius: 50%;
            filter: blur(2px);
            animation: spin 8s linear infinite;
        }
        
        .accretion-disk-1 {
            width: 500px;
            height: 500px;
            border: 15px solid;
            border-image: linear-gradient(90deg, 
                rgba(0, 255, 200, 0.8),
                rgba(0, 200, 255, 0.6),
                rgba(100, 200, 255, 0.4),
                rgba(0, 255, 200, 0.8)
            ) 1;
            box-shadow: 
                inset 0 0 40px rgba(0, 255, 200, 0.6),
                0 0 60px rgba(0, 255, 200, 0.4);
        }
        
        .accretion-disk-2 {
            width: 420px;
            height: 420px;
            border: 12px solid;
            border-image: linear-gradient(90deg,
                rgba(0, 200, 255, 0.7),
                rgba(100, 200, 255, 0.5),
                rgba(0, 255, 200, 0.6),
                rgba(0, 200, 255, 0.7)
            ) 1;
            box-shadow: 
                inset 0 0 30px rgba(0, 200, 255, 0.5),
                0 0 40px rgba(0, 200, 255, 0.3);
            animation: spin 10s linear infinite reverse;
        }
        
        .accretion-disk-3 {
            width: 340px;
            height: 340px;
            border: 10px solid;
            border-image: linear-gradient(90deg,
                rgba(100, 200, 255, 0.6),
                rgba(0, 255, 200, 0.7),
                rgba(0, 200, 255, 0.5),
                rgba(100, 200, 255, 0.6)
            ) 1;
            box-shadow: 
                inset 0 0 20px rgba(100, 200, 255, 0.5),
                0 0 30px rgba(0, 255, 200, 0.2);
        }
        
        /* Anillo de evento del horizonte */
        .event-horizon {
            position: absolute;
            width: 200px;
            height: 200px;
            background: radial-gradient(circle at 35% 35%, rgba(20, 50, 100, 0.9), rgba(5, 10, 30, 0.95), #000);
            border-radius: 50%;
            box-shadow: 
                0 0 40px rgba(0, 255, 200, 0.4),
                inset 0 0 40px rgba(0, 100, 150, 0.6),
                0 0 80px rgba(0, 200, 255, 0.2);
            filter: brightness(0.8);
        }
        
        /* Corazones anulares */
        .heart-ring {
            position: absolute;
            animation: pulse 2s ease-in-out infinite;
        }
        
        .heart {
            width: 30px;
            height: 30px;
            position: relative;
            display: inline-block;
            filter: drop-shadow(0 0 3px rgba(0, 255, 200, 0.6));
        }
        
        .heart::before,
        .heart::after {
            content: '';
            position: absolute;
            width: 30px;
            height: 45px;
            background: currentColor;
            border-radius: 30px 30px 0 0;
            left: 30px;
            top: 0;
        }
        
        .heart::before {
            left: -15px;
            transform: rotate(-45deg);
            transform-origin: 0 100%;
        }
        
        .heart::after {
            left: 0;
            transform: rotate(45deg);
            transform-origin: 100% 100%;
        }
        
        .heart-ring-1 {
            width: 280px;
            height: 280px;
            animation-delay: 0s;
        }
        
        .heart-ring-1 .heart {
            color: rgba(0, 255, 200, 0.9);
            text-shadow: 0 0 10px rgba(0, 255, 200, 0.8);
        }
        
        .heart-ring-2 {
            width: 360px;
            height: 360px;
            animation-delay: 0.3s;
        }
        
        .heart-ring-2 .heart {
            color: rgba(0, 200, 255, 0.85);
            text-shadow: 0 0 10px rgba(0, 200, 255, 0.7);
        }
        
        .heart-ring-3 {
            width: 440px;
            height: 440px;
            animation-delay: 0.6s;
        }
        
        .heart-ring-3 .heart {
            color: rgba(100, 200, 255, 0.8);
            text-shadow: 0 0 10px rgba(100, 200, 255, 0.6);
        }
        
        /* Posicionar corazones en círculo */
        .heart-wrapper {
            position: absolute;
            width: 100%;
            height: 100%;
        }
        
        .heart-item {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
        }
        
        /* Animaciones */
        @keyframes spin {
            from {
                transform: rotate(0deg);
            }
            to {
                transform: rotate(360deg);
            }
        }
        
        @keyframes pulse {
            0%, 100% {
                opacity: 0.7;
                transform: scale(1);
            }
            50% {
                opacity: 1;
                transform: scale(1.05);
            }
        }
        
        /* Texto de título */
        .title {
            position: absolute;
            top: 30px;
            font-size: 28px;
            color: rgba(0, 255, 200, 0.9);
            text-shadow: 0 0 20px rgba(0, 255, 200, 0.6);
            font-weight: bold;
            letter-spacing: 2px;
        }
        
        .subtitle {
            position: absolute;
            bottom: 30px;
            font-size: 14px;
            color: rgba(0, 200, 255, 0.7);
            text-shadow: 0 0 10px rgba(0, 200, 255, 0.4);
            letter-spacing: 1px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="title">GARGANTÚA</div>
        
        <!-- Círculos de acreción -->
        <div class="accretion-disk accretion-disk-1"></div>
        <div class="accretion-disk accretion-disk-2"></div>
        <div class="accretion-disk accretion-disk-3"></div>
        
        <!-- Anillos de corazones -->
        <div class="heart-ring heart-ring-1">
            <div class="heart-wrapper" id="hearts1"></div>
        </div>
        
        <div class="heart-ring heart-ring-2">
            <div class="heart-wrapper" id="hearts2"></div>
        </div>
        
        <div class="heart-ring heart-ring-3">
            <div class="heart-wrapper" id="hearts3"></div>
        </div>
        
        <!-- Evento horizonte (agujero negro) -->
        <div class="event-horizon"></div>
        
        <div class="subtitle">~ Interstellar ~</div>
    </div>
    
    <script>
        // Función para crear corazones en anillo
        function createHeartRing(elementId, numHearts) {
            const container = document.getElementById(elementId);
            for (let i = 0; i < numHearts; i++) {
                const angle = (i / numHearts) * Math.PI * 2;
                const heart = document.createElement('div');
                heart.className = 'heart-item';
                
                const radius = 100; // relativo a su contenedor
                const x = Math.cos(angle) * radius;
                const y = Math.sin(angle) * radius;
                
                heart.style.transform = `translate(calc(-50% + ${x}px), calc(-50% + ${y}px))`;
                heart.innerHTML = '<div class="heart"></div>';
                container.appendChild(heart);
            }
        }
        
        // Crear corazones en los tres anillos
        createHeartRing('hearts1', 8);  // 8 corazones en el primer anillo
        createHeartRing('hearts2', 10); // 10 corazones en el segundo anillo
        createHeartRing('hearts3', 12); // 12 corazones en el tercer anillo
    </script>
</body>
</html># AGUJERO-NEGRO-AZUL-