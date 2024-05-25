```
<div *ngIf="events.length === 0; else showContent">
  <!-- Show header when myEvent is an empty array -->
  <h2>No Events</h2>
</div>

<ng-template #showContent>
  <!-- Show content when myEvent is not an empty array -->
  <div *ngFor="let event of myEvent">
    <!-- Render each event here -->
    <p>{{ event.name }}</p>
  </div>
</ng-template>


```
