# test


npm install yarn -g
npm install git
npm install -g @angular/cli
ng new MovieDB
npm install
npm install --save @angular/material @angular/cdk
npm install --save @angular/animations
ng serve

ng g component home
ng g service my-new-service
ng g class my-new-class
ng g enum my-new-enum
ng g module my-module
ng g interface my-new-interface
ng g guard my-new-guard



npm install

npm update -g @angular/cli


<mat-toolbar class="example-header">Header</mat-toolbar>

  <mat-sidenav-container class="example-container">
    <mat-sidenav mode="side" opened="true" class="example-sidenav" >
      <table style="width: 100%;  text-align: center">
        <tr>
          <td>
              <a  mat-button routerLink=".">Link</a>
          </td>
        </tr> <tr>
            <td>
                <a  mat-button routerLink=".">Link</a>
            </td>
          </tr>
      </table>
  </mat-sidenav>

    <mat-sidenav-content class="example-sidenav-content" >
      <router-outlet></router-outlet>
    </mat-sidenav-content>
  </mat-sidenav-container>


import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';
import { AppComponent } from './app.component';
import {platformBrowserDynamic} from '@angular/platform-browser-dynamic';
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';
import { RouterModule, Routes } from '@angular/router';
import { FlexLayoutModule } from '@angular/flex-layout';

import {
  MatAutocompleteModule,
  MatBadgeModule,
  MatBottomSheetModule,
  MatButtonModule,
  MatButtonToggleModule,
  MatCardModule,
  MatCheckboxModule,
  MatChipsModule,
  MatDatepickerModule,
  MatDialogModule,
  MatDividerModule,
  MatExpansionModule,
  MatGridListModule,
  MatIconModule,
  MatInputModule,
  MatListModule,
  MatMenuModule,
  MatNativeDateModule,
  MatPaginatorModule,
  MatProgressBarModule,
  MatProgressSpinnerModule,
  MatRadioModule,
  MatRippleModule,
  MatSelectModule,
  MatSidenavModule,
  MatSliderModule,
  MatSlideToggleModule,
  MatSnackBarModule,
  MatSortModule,
  MatStepperModule,
  MatTableModule,
  MatTabsModule,
  MatToolbarModule,
  MatTooltipModule,
  MatTreeModule,
  MatTableDataSource
} from '@angular/material';
import { MoviesComponent } from './movies/movies.component';
import { GenresComponent } from './genres/genres.component';
import { HomeComponent } from './home/home.component';

const appRoutes: Routes = [
  {
    path: 'movies',
    component: MoviesComponent,
    data: { title: 'Movies List' }
  },
  {
    path: 'genres',
    component: GenresComponent,
    data: { title: 'Genres' }
  },
  { path: '**', component: HomeComponent }
];

@NgModule({
  declarations: [
    AppComponent,
    MoviesComponent,
    GenresComponent,
    HomeComponent
  ],
  imports: [
    BrowserModule,
    MatGridListModule,
    MatSidenavModule,
    MatToolbarModule,
    MatCardModule,
    BrowserAnimationsModule,
    FlexLayoutModule,
    MatMenuModule,
    MatButtonModule,
    MatTableModule    ,
    HttpClientModule,
    RouterModule.forRoot(
      appRoutes
      //{ enableTracing: true } // <-- debugging purposes only
    )
  ],
  providers: [],
  bootstrap: [AppComponent]
  
})
export class AppModule { }







 




{
    "version": "0.2.0",
    "configurations": [
      {
        "name": "ng serve",
        "type": "chrome",
        "request": "launch",
        "url": "http://localhost:4200/#",
        "webRoot": "${workspaceRoot}"
      },
      {
        "name": "ng test",
        "type": "chrome",
        "request": "launch",
        "url": "http://localhost:9876/debug.html",
        "webRoot": "${workspaceRoot}"
      },
      {
        "name": "ng e2e",
        "type": "node",
        "request": "launch",
        "program": "${workspaceRoot}/node_modules/protractor/bin/protractor",
        "protocol": "inspector",
        "args": ["${workspaceRoot}/protractor.conf.js"]
      }      
    ]
  }


Grid

import { Component, OnInit } from '@angular/core';
import { MoviesService } from './movies.service';
import {MatTableDataSource} from '@angular/material';


@Component({
  selector: 'app-movies',
  templateUrl: './movies.component.html',
  styleUrls: ['./movies.component.css']
})
export class MoviesComponent implements OnInit {

  
  movies: any[]
  displayedColumns : string[]
  dataSource : any;
  constructor(private moviesService: MoviesService) { 
    
  }

  ngOnInit() {
    try {
      this.moviesService.GetAll().subscribe(downloading => {
       this.movies = downloading;
       this.dataSource = new MatTableDataSource(this.movies);
   },(error)=>{
    var test = error;
   });
    this.displayedColumns = ['id', 'title', 'description', 'year', 'ratingId'];
    
   } catch (error) {
     
   }
  }

  GetAll()
  {
   
   
  }
}


import { Injectable } from '@angular/core';
import { BaseServiceService } from '../base-service.service';
import { HttpClient,HttpHeaders } from '@angular/common/http';
import { Observable } from 'rxjs';
import { map} from 'rxjs/operators';
@Injectable({
  providedIn: 'root'
})
export class MoviesService {

  api : string;
  constructor(baseApi : BaseServiceService, private http: HttpClient) {
      this.api = baseApi.api;
   }

   GetAll()   {
   return this.http.get<any[]>(this.api + "/movies/getall/");
   }

  

  }


<table mat-table [dataSource]="dataSource" class="mat-elevation-z8">
    
      <!--- Note that these columns can be defined in any order.
            The actual rendered columns are set as a property on the row definition" -->
    
      <ng-container matColumnDef="id">
        <th mat-header-cell *matHeaderCellDef> id </th>
        <td mat-cell *matCellDef="let element"> {{element.id}} </td>
      </ng-container>
    
      <ng-container matColumnDef="title">
        <th mat-header-cell *matHeaderCellDef> title </th>
        <td mat-cell *matCellDef="let element"> {{element.title}} </td>
      </ng-container>
    
      <ng-container matColumnDef="description">
        <th mat-header-cell *matHeaderCellDef> description </th>
        <td mat-cell *matCellDef="let element"> {{element.description}} </td>
      </ng-container>
    
      <ng-container matColumnDef="year">
        <th mat-header-cell *matHeaderCellDef> year </th>
        <td mat-cell *matCellDef="let element"> {{element.year}} </td>
      </ng-container>
    
      <ng-container matColumnDef="ratingId">
          <th mat-header-cell *matHeaderCellDef> ratingId </th>
          <td mat-cell *matCellDef="let element"> {{element.ratingId}} </td>
        </ng-container>

      <tr mat-header-row *matHeaderRowDef="displayedColumns"></tr>
      <tr mat-row *matRowDef="let row; columns: displayedColumns;"></tr>
    </table>
