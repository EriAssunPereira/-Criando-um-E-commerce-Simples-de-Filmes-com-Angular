# Criando-um-E-commerce-Simples-de-Filmes-com-Angular

Vamos criar um projeto de e-commerce simples de filmes utilizando Angular e TypeScript. Este projeto irá explorar desde a configuração básica até a implementação de funcionalidades essenciais para um e-commerce. Vou dividir o projeto em módulos para facilitar o entendimento e manter.

### Módulo 1: Configuração Básica do Projeto Angular

1. **Configuração do Ambiente de Desenvolvimento**: Certifique-se de ter o Node.js e o Angular CLI instalados globalmente.

   ```bash
   # Instalação do Angular CLI
   npm install -g @angular/cli
   ```

2. **Criando um Novo Projeto Angular**: Inicie um novo projeto Angular chamado `film-ecommerce`.

   ```bash
   ng new film-ecommerce --style=scss --routing=true
   cd film-ecommerce
   ```

### Módulo 2: Estrutura e Componentes Iniciais

1. **Criação de Componentes**: Crie componentes para o cabeçalho, listagem de filmes e detalhes de filme.

   ```bash
   ng generate component header
   ng generate component movie-list
   ng generate component movie-details
   ```

2. **Definição de Rotas**: Configure rotas no arquivo `app-routing.module.ts` para navegação entre os componentes.

   ```typescript
   // app-routing.module.ts
   import { NgModule } from '@angular/core';
   import { Routes, RouterModule } from '@angular/router';
   import { MovieListComponent } from './movie-list/movie-list.component';
   import { MovieDetailsComponent } from './movie-details/movie-details.component';

   const routes: Routes = [
     { path: '', component: MovieListComponent },
     { path: 'movie/:id', component: MovieDetailsComponent },
     { path: '**', redirectTo: '' }
   ];

   @NgModule({
     imports: [RouterModule.forRoot(routes)],
     exports: [RouterModule]
   })
   export class AppRoutingModule { }
   ```

### Módulo 3: Serviços e Integração com API

1. **Criando um Serviço para Filmes**: Crie um serviço para gerenciar dados de filmes e integre com uma API (fictícia neste exemplo).

   ```bash
   ng generate service movie
   ```

   ```typescript
   // movie.service.ts
   import { Injectable } from '@angular/core';
   import { HttpClient } from '@angular/common/http';
   import { Observable } from 'rxjs';
   import { Movie } from './movie.model';

   @Injectable({
     providedIn: 'root'
   })
   export class MovieService {
     private apiUrl = 'http://localhost:3000/movies'; // Exemplo de URL da API

     constructor(private http: HttpClient) { }

     getMovies(): Observable<Movie[]> {
       return this.http.get<Movie[]>(this.apiUrl);
     }

     getMovieById(id: number): Observable<Movie> {
       return this.http.get<Movie>(`${this.apiUrl}/${id}`);
     }
   }
   ```

2. **Definindo um Modelo de Filme**: Crie um modelo TypeScript para representar os dados dos filmes.

   ```typescript
   // movie.model.ts
   export interface Movie {
     id: number;
     title: string;
     director: string;
     year: number;
     description: string;
     imageUrl: string;
     price: number;
   }
   ```

### Módulo 4: Componentes e Templates

1. **Componente de Listagem de Filmes**: Implemente a listagem de filmes com um componente Angular.

   ```html
   <!-- movie-list.component.html -->
   <div *ngFor="let movie of movies">
     <h3>{{ movie.title }}</h3>
     <p>{{ movie.director }}</p>
     <p>{{ movie.year }}</p>
     <button (click)="goToDetails(movie.id)">Detalhes</button>
   </div>
   ```

   ```typescript
   // movie-list.component.ts
   import { Component, OnInit } from '@angular/core';
   import { Movie } from '../movie.model';
   import { MovieService } from '../movie.service';
   import { Router } from '@angular/router';

   @Component({
     selector: 'app-movie-list',
     templateUrl: './movie-list.component.html',
     styleUrls: ['./movie-list.component.scss']
   })
   export class MovieListComponent implements OnInit {
     movies: Movie[];

     constructor(private movieService: MovieService, private router: Router) { }

     ngOnInit(): void {
       this.movieService.getMovies().subscribe(movies => {
         this.movies = movies;
       });
     }

     goToDetails(id: number): void {
       this.router.navigate(['movie', id]);
     }
   }
   ```

### Módulo 5: Estilização e Finalização

1. **Estilização com CSS ou SCSS**: Estilize os componentes e adicione responsividade conforme necessário.

   ```scss
   /* movie-list.component.scss */
   div {
     background-color: #f0f0f0;
     padding: 20px;
     margin-bottom: 10px;
     border-radius: 8px;
     box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
   }

   button {
     background-color: #007bff;
     color: #fff;
     border: none;
     padding: 8px 16px;
     cursor: pointer;
     border-radius: 4px;
   }

   button:hover {
     background-color: #0056b3;
   }
   ```

2. **Integração Completa**: Continue expandindo o projeto adicionando mais funcionalidades como carrinho de compras, checkout, etc.

Este projeto básico de e-commerce de filmes utilizando Angular e TypeScript serve como um ponto de partida para explorar funcionalidades mais avançadas e aprimorar suas habilidades com esta poderosa stack frontend. Podemos expandir o projeto adicionando filtros de pesquisa, paginac.
