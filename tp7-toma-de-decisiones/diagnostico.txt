(defrule leer-estado-enfermedad
	=>
	(printout t "Indique el estatado de la enfermedad (incipiente/avanzado/terminal): ")
	(assert (enfermedad(read)))
)

(defrule leer-n-dosis
	(enfermedad ?)
	=>
	(printout t "Indique el numero de dosis empleadas (bajo/normal/elevado): ")
	(assert (n-dosis(read)))
)

(defrule leer-estado-fisico
	(enfermedad ?)
	=>
	(printout t "Cual considera que es el estado fisico? (fuerte/debil): ")
	(assert (estado-fisico(read)))
)

(defrule enfermedad-avanzado
	(enfermedad ?e)
	=>
	(if (eq ?e avanzado)
	then
		(assert (diagnostico curacion))
	)
)

(defrule enfermedad-incipiente-n-dosis
	(enfermedad ?e)
	(n-dosis ?n)
	=>
	(if (eq ?e incipiente)
	then
		(if (eq ?n bajo)
		then
			(assert (diagnostico curacion))
		else
			(assert (diagnostico defuncion))
		)
	)
)

(defrule enfermedad-terminal-estado-fisico
	(enfermedad ?e)
	(estado-fisico ?f)
	=>
	(if (eq ?e terminal)
	then
		(if (eq ?f debil)
		then
			(assert (diagnostico curacion))
		else
			(assert (diagnostico defuncion))
		)
	)
)

(defrule diagnosticar
	(diagnostico ?d)
	(enfermedad ?)
	(n-dosis ?)
	(estado-fisico ?)
	=>
	(printout t ?d ":este es su diagnostico.")
) 