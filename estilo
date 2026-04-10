document.addEventListener("DOMContentLoaded", () => {
    const ramos = document.querySelectorAll(".ramo");

    // Función principal para verificar dependencias
    function actualizarMalla() {
        let cambiosRealizados = false;

        ramos.forEach(ramo => {
            // Leer los requisitos del atributo data-req (si no tiene, es un array vacío)
            const requisitosStr = ramo.getAttribute("data-req") || "[]";
            const requisitos = JSON.parse(requisitosStr);
            
            let requisitosCumplidos = true;

            // Revisar si todos los requisitos están aprobados
            for (let reqId of requisitos) {
                const reqRamo = document.getElementById(reqId);
                if (reqRamo && !reqRamo.classList.contains("aprobado")) {
                    requisitosCumplidos = false;
                    break;
                }
            }

            // Aplicar o quitar la clase "bloqueado"
            if (!requisitosCumplidos) {
                if (!ramo.classList.contains("bloqueado")) {
                    ramo.classList.add("bloqueado");
                    cambiosRealizados = true;
                }
                // Si por alguna razón estaba aprobado pero perdió sus requisitos
                if (ramo.classList.contains("aprobado")) {
                    ramo.classList.remove("aprobado");
                    cambiosRealizados = true;
                }
            } else {
                if (ramo.classList.contains("bloqueado")) {
                    ramo.classList.remove("bloqueado");
                    cambiosRealizados = true;
                }
            }
        });

        // Si hubieron bloqueos/desbloqueos en cadena, volvemos a evaluar
        if (cambiosRealizados) {
            actualizarMalla();
        }
    }

    // Agregar el evento de clic a cada ramo
    ramos.forEach(ramo => {
        ramo.addEventListener("click", () => {
            // Solo permite interactuar si el ramo NO está bloqueado
            if (!ramo.classList.contains("bloqueado")) {
                ramo.classList.toggle("aprobado");
                // Una vez que cambia el estado, re-calculamos la malla completa
                actualizarMalla();
            }
        });
    });

    // Inicializar la malla por primera vez al cargar la página
    actualizarMalla();
});
