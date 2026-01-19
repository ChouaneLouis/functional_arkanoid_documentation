## TODO
- [x] Interface
- [ ] Contrat exact des cas d'erreur de Physic
- [ ] Implantation de Physic avec : `type ('t * 'a) pool = ('t body * 'a) list`
- [ ] Test unitaire : cas critique
	- [ ] collision multiple : annulé le dernier mouvement fait
	- [ ] rebond selon la face touché
	- [ ] rebond sur le coin
	- [ ] rebond sur un objet physique => rebond symétrique
- [ ] Implantation de Physic avec : `type ('t * 'a) pool = ('t body * 'a) tree`
## INTERFACE
```ocaml
open Geometry
module type Physic (V : Vector) =
sig
	(* élément physique de la scene :
	 * forme, position, vitesse, accélération, peu rebondir *)
	type _ body = (Shape.t * V.t * V.t * V.t * bool) (* public *)
	(* ensemble de paire (élément physique, obj 'a) *)
	type (_ * 'a) pool
	(* type fantome destiné au typage de body *)
	type stat = unit (* élément statique *)
	type dyna = unit (* élément mobile *)
	
	(* Pool statique vide *)
	val empty_stat_pool : stat pool
	
	(* Pool dynamique vide *)
	val empty_dyna_pool : dyna pool
	
	(* Ajoute un body a une pool *)
	(* return : (nouv pool * indice du body créer) *)
	val add : ('t * 'a) pool -> 't body -> 'a -> ('t * 'a) pool
	
	(* N-eme élément d'une pool *)
	val get : ('t * 'a) pool -> int -> ('t body * 'a)
	
	(* Modifie le n-eme élément d'une pool *)
	val set : ('t * 'a) pool -> int -> ('t body * 'a) -> ('t * 'a) pool
	
	(* Retire le n-eme élément d'une pool *)
	val pop : ('t * 'a) pool -> int -> ('t * 'a) pool
	
	(* Avance d'un pas de temps avec gestion des rebonds
	 * return : (nouvelle pool dynamique *
	 *   liste des collisions aillant eu lieu *
	 *   liste des objets ayant subi une collision) *)
	val update : (dyna * 'a) pool -> (stat * 'a) pool -> float
		-> ((dyna * 'a) pool * int list * 'a list * int list * 'a list)
	
	(* Appel une fonction sur chaque body d'une pool *)
	val iter : ('t * 'a) pool -> ('t body -> 'a -> unit) -> unit
end
```
