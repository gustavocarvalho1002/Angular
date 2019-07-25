# Angular
Repositório para colocar anotações importante em markdown sobre operações dentro do framework Angular.

## 1 Observable vs Promise
#### 1.1 Implementação de um promise
```typescript
getEstudantes(): Promise<Estudante[]>{
  return fetch(url)
  .then(res=>res.json())
  .catch(err=>{
     throw new Error(err.message);  
   });
}
```
#### 1.2 Implementação de um observable

``` typescript
@Injectable()
class EstudanteService {
 ...
 getEstudantes(): Observable<Estudante[]> {
    return this.http.get(url)
                    .map(res=>res.json())
                    .catch(err=> Observable.throw(err.message));
 } 
 ...
}
```

#### 1.3 Subscribe(O metodo que vou me "inscrever" é o do item 1.2)
``` typescript
import { EstudanteService } from 'user.service';
@Component({
  /* Propriedades do componente*/
})
class EstudanteComponent {
  ...
  constructor(private estudanteService: EstudanteService){}
  private estudantes: Estudante[]; // Lista de usuários
  /* Neste método chamamos a função estudanteService.getEstudantes, que nos retorna um Observable contendo um array de estudantes, então atribuímos ao this.estudantes */
  getEstudantes() {
    this.estudanteService.getUsers()
                    .subscribe(
                      dados => this.estudantes = dados,
                      error => /* Tratamos erros aqui :) */);
  }
  ...
}
```
<br>
<br>
<br>
