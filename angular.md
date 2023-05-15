classes for small green button: btn btn-success btn-sm

built in directive that has instance of each input in template driven form: ngForm

actual product to be demoed to client each sprint: sprint demo

#app-routing.module.ts
```Typescript
const routes: Routes = [
	{path: 'gamesconsole', component: GamesConsoleComponent},
	{path: '', redirectTo: '/gamesconsole', pathMatch: 'full'},
	{path: 'order/:consoleName', component: OrderComponent},
	{path: '**', component: GamesConsoleComponent, pathMatch: 'full'}
];
```

#games-console.component.ts
```Typescript
buy() {
	this.router.navigate(['/order', this.console.consoleName]);
}
```

#games-console.component.html
```HTML
<div class="row">
	<div class="col-md-4" *ngFor="let console of consoles">
		<div class="card">
			<div class="card-header">
				<h3>{{console.consoleName}}</h3>
			</div>
			<div class="card-body">
				<img src="{{console.imageUrl}}" alt="{{console.consoleName}}" class="img-fluid">
				<p>{{console.description}}</p>
				<a [routerLink]="['/order', console.consoleName]" class="btn btn-success btn-sm">Order</a>
			</div>
		</div>
	</div>
```

#order.component.ts
```Typescript

this.consoleName = this.route.snapshot.params['consoleName'];

this.orderForm = new FormGroup({
	consoleName: new FormControl({value: this.consoleName, disabled: true}, Validators.required),
	mobileNumber: new FormControl('', [Validators.required, Validators.pattern('[0-9]{10}')]),
	address: new FormControl('', [Validators.required, this.validateAddress]),
	quantity: new FormControl(1, [Validators.required, Validators.min(1), Validators.max(3)])
});


orderGamesConsole() {


	this.orderService.orderGamesConsole(orderForm).subscribe(
		(response)=> {
			this.successMessage = `${response.consoleName} is ordered successfully.`;
		}

		(error)=> {
			this.errorMessage = 'Network issue! Ordering failed.'
		}
	)
}
```

#order.service.ts
```Typescript
return this.http.post<OrderResponse>(this.orderUrl, orderForm);
```

#order.component.html
```HTML
<form [formGroup]='orderForm' (ngSubmit)='orderGamesConsole()'>
	<div class="form-group">
		<label for="consoleName">Console Name</label>
		<input type="text" id="consoleName" class="form-control" formControlName="consoleName">
		
	</div>
	<div class="form-group">
		<label for="mobileNumber">Mobile Number</label>
		<input type="text" id="mobileNumber" class="form-control" formControlName="mobileNumber">
		<span *ngIf="orderForm.get('mobileNumber').errors.required && 
		orderForm.get('mobileNumber').touched">Mobile Number is required</span>
		<span *ngIf="orderForm.get('mobileNumber').errors.pattern 
		&& orderForm.get('mobileNumber').diry">Mobile Number should be 10 digits</span>
	</div>
	<div class="form-group">
		<label for="address">Address</label>
		<textarea id="address" class="form-control" formControlName="address"></textarea>
		<span *ngIf="orderForm.get('address').errors.required &&
		orderForm.get('address').touched">Address is required</span>
		<span *ngIf="orderForm.get('address').errors.addressError &&
		orderForm.get('address').touched">Address should be in the format: city, state, country</span>
	</div>
	<div class="form-group">
		<label for="quantity">Quantity</label>
		<input type="number" id="quantity" class="form-control" formControlName="quantity">
		<span *ngIf="orderForm.get('quantity').errors.required &&
		orderForm.get('quantity').touched">Quantity is required</span>
		<span *ngIf="orderForm.get('quantity').errors.min &&
		orderForm.get('quantity').touched">Quantity should be minimum 1</span>
	</div>
	<!-- disable button if form is invalid -->
	<button type="submit" class="btn btn-success btn-sm" [disabled]="orderForm.invalid">Order</button>
