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




ngOnInit(): void {
  this.uploadService.gridRefreshEvent.subscribe(() => {
    if (this.gridApi) {
      const datasource = this.getDocumentsDataSource();

      if (this.gridApi.getDisplayedRowCount() === 0) {
        // 🔄 Force full reload if no rows are present
        this.gridApi.setServerSideDatasource(datasource);
      } else {
        // 🔁 Otherwise just refresh cache (faster, keeps scroll state)
        this.gridApi.refreshServerSideStore({ purge: true });
      }
    }
  });
}
