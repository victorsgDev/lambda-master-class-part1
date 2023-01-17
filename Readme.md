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

## Comparator<T>:

    Recibe dos argumentos y retorna un int.
    
   - Método funcional:
    
    int compare(T t1, T t2);
      
   - Métodos:
    
    static <T, U extends Comparable<? super U>> Comparator<T> comparing(Function<T, U> keyExtractor) {
         Objects.requireNonNull(keyExtractor);
         return (p1, p2) -> {
             U u1 = keyExtractor.apply(p1);
             U u2 = keyExtractor.apply(p2);
             return u1.compareTo(u2);
         };
     }
    
        
