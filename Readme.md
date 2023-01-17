# FUNCTIONAL INTERFACES @FunctionalInterface:
## Consumer<T>: 

    Recibe un argumento pero no retorna nada.
    
   - Método funcional:
    
    void accept(T t);
    
   - Método default: 
    
    default Consumer<T> andThen(Consumer<T> other) {
          return (T t) -> { this.accept(t); other.accept(t);};
    }
 
 ## Predicate<T>: 
  
    Recibe un argumento y retorna un boolean.
    
   -  Método funcional:
    
    boolean test(T t);
    
   -  Métodos default:
    
    default Predicate<T> negate() {
        return t -> !this.test(t);        
    }
    
    default Predicate<T> and(Predicate<T> other) {
        Objects.requireNonNull(other);        
        return t -> this.test(t) && other.test(t);      
    }

    default Predicate<T> or(Predicate<T> other) {    
        Objects.requireNonNull(other);        
        return t -> this.test(t) || other.test(t);        
    }
    
    default Predicate<T> isEqual(Object targetRef){        
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);    
    }
