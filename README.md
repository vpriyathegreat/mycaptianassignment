ngOnInit(): void {
  this.uploadService.gridRefreshEvent.subscribe(() => {
    if (this.gridApi) {
      console.log("🔄 Refresh event received. Resetting datasource...");

      const dataSource = this.getDocumentsDataSource();

      if (dataSource) {
        console.log("✅ Datasource created. Forcing grid reload...");
        this.gridApi.setServerSideDatasource(dataSource);

        // Force first row request to trigger fetch
        this.gridApi.refreshServerSideStore({ purge: true });
        console.log("⚡ Server-side store purged & refreshed.");
      } else {
        console.warn("⚠️ No datasource available. Grid not refreshed.");
      }
    } else {
      console.warn("⚠️ Grid API not ready. Cannot refresh grid.");
    }
  });
}
