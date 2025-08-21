ngOnInit(): void {
  this.uploadService.gridRefreshEvent.subscribe(() => {
    if (this.gridApi) {
      // ✅ If grid already has data → refresh
      this.gridApi.refreshServerSideStore({ purge: true });

      // ✅ If grid has 0 rows → reset datasource & fetch
      if (this.gridApi.getDisplayedRowCount() === 0) {
        this.gridApi.setServerSideDatasource(this.getDocumentsDataSource());
      }
    }
  });
}
