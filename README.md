public onGridReady(params: any): void {
  this.gridApi = params.api;
  this.gridColumnApi = params.columnApi;

  console.log('[Grid] Ready ✅');

  // Always set initial datasource when grid is ready
  this.gridApi.setServerSideDatasource(this.getDocumentsDataSource());

  // Subscribe to refresh events safely
  this.uploadService.gridRefreshEvent.subscribe(() => {
    console.log('[Grid Refresh] Event received ✅');

    if (this.gridApi) {
      console.log('[Grid Refresh] Resetting server-side datasource');
      this.gridApi.setServerSideDatasource(this.getDocumentsDataSource());
    } else {
      console.warn('[Grid Refresh] Grid API not ready yet ❌');
    }
  });
}
